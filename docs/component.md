# `src/component.js`

## Overview

This document describes the class component base used by `Component` in Preact. It covers how the module initializes a component instance, schedules updates, renders output, and keeps DOM pointers accurate while the tree changes.

## Prerequisites

- Familiarity with `Component` from `preact`
- Basic understanding of `render()` and state updates

## Exports

The module defines `BaseComponent`, which `src/index.js` exposes as `Component`.

- `BaseComponent(props, context)` stores the incoming `props` and `context`, then initializes `_bits` to `0`.
- `BaseComponent.prototype.setState(update, callback)` merges a partial state update into the pending state snapshot.
- `BaseComponent.prototype.forceUpdate(callback)` schedules a render without consulting `shouldComponentUpdate()`.
- `BaseComponent.prototype.render` defaults to `Fragment`.
- `enqueueRender(component)` adds a component to the render queue.
- `resetRenderCount()` clears the scheduler counter used by the render queue.
- `getDomSibling(vnode, childIndex)` finds the next DOM node that follows a vnode subtree.
- `updateParentDomPointers(vnode)` refreshes ancestor DOM pointers after a render changes the output tree.

## Component construction

`BaseComponent` gives each instance the public `props` and `context` values it receives at construction time. It also starts `_bits` at `0` so the scheduler can mark the instance as dirty or forced later in the update cycle.

The public `Component` class inherits this behavior. A class component extends it and implements `render()` to describe the output for the current `props`, `state`, and `context`.

```jsx
import { Component, h } from 'preact';

class Counter extends Component {
  constructor(props, context) {
    super(props, context);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState(state => ({ count: state.count + 1 }));
  };

  render(_, state) {
    return <button onClick={this.increment}>{state.count}</button>;
  }
}
```

## `setState(update, callback)`

`setState()` prepares a pending state update and queues a re-render when the component is already mounted.

- When `update` is an object, `setState()` merges its fields into the pending state.
- When `update` is a function, `setState()` calls it with a shallow copy of the current pending state and the current `props`, then merges the returned object.
- When `update` is falsy, `setState()` returns without changing the state.
- When the component has not mounted yet, `setState()` only updates the pending state snapshot.
- When the component has mounted, `setState()` queues `callback` in `_stateCallbacks` and adds the component to the render queue.

The method keeps the first pending update in `_nextState` and reuses that object for later updates in the same cycle.

## `forceUpdate(callback)`

`forceUpdate()` schedules a render even when the normal update checks would block it.

- When the component has not mounted yet, `forceUpdate()` does nothing.
- When the component has mounted, `forceUpdate()` marks the instance with `COMPONENT_FORCE` so the renderer skips `shouldComponentUpdate()`.
- When `callback` exists, `forceUpdate()` adds it to `_renderCallbacks`.
- After the method marks the component, it adds the component to the render queue.

## Default `render()` behavior

The base class assigns `Fragment` to `render()`. That default keeps the component from producing its own output and gives subclasses a clear starting point: override `render()` when the component should return visible content.

## Render queue and rerender flow

`enqueueRender()` starts the update cycle.

1. It marks the component as dirty with `COMPONENT_DIRTY`.
2. It adds the component to `rerenderQueue`.
3. It schedules `process()` with the configured `options.debounceRendering` callback or `queueMicrotask()`.

`process()` drains the queue in depth order.

- It sorts queued components by vnode depth when new work enters the queue during a flush.
- It processes parents before children so related updates finish in a stable order.
- It removes each queued component with `shift()` and renders only dirty entries.
- It clears the queue and the scheduler counter at the end of the flush.

`renderComponent()` performs the actual rerender for one component.

- It clones the current vnode and increments the clone revision.
- It calls `diff()` to compare the old and new vnode trees.
- It calls `commitRoot()` to finish DOM updates and ref callbacks.
- It clears the stale vnode and DOM links on the old tree.
- It calls `updateParentDomPointers()` when the rendered DOM node changes position.

## DOM sibling lookup and pointer maintenance

`getDomSibling()` helps the diffing code place new DOM nodes in the right spot.

- When the caller passes no child index, the function resumes the search from the vnode's next sibling.
- When the vnode has children, the function returns the first child that already owns a DOM node.
- When the subtree has no direct DOM node and the vnode represents a component, the function continues the search from the component's sibling chain.

`updateParentDomPointers()` repairs ancestor pointers after a rerender.

- It walks up through parent components.
- It clears each ancestor's `_dom` pointer.
- It restores `_dom` from the first child that still points at a rendered DOM node.
- It repeats the process until it reaches the top of the component chain.

## Reference

- Extend `Component` from `preact`.
- Implement `render()` to return the vnode tree for the current state.
- Use `setState()` for queued updates and `forceUpdate()` for an immediate rerender request.
