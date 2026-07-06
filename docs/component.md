# Component module reference

## Overview

`src/component.js` defines the class component base and the render scheduler that keeps mounted instances in sync with the DOM. Consumers import `Component` from `src/index.js`; that entry point re-exports `BaseComponent` under the public name.

```js
import { Component } from 'preact';
```

This module also supplies the internal helpers that locate DOM siblings, rerender dirty components, and repair parent DOM pointers after a render changes the tree shape.

## Public API

### `BaseComponent(props, context)`

`BaseComponent` stores the initial `props` and `context`, then initializes the internal bit field at `0`. The constructor leaves `state` alone, so subclasses can assign their own initial state later.

### `setState(update, callback)`

`setState` merges a partial state update into a lazily created `_nextState` object.

- The first call clones `this.state` into `_nextState`.
- Later calls reuse the same pending object until the render cycle consumes it.
- A function updater receives a writable copy of the current pending state and the current props.
- A falsy return value stops the update and leaves the queue untouched.
- A truthy object merges into the pending state.

`setState` only schedules work after the component mounts. Before mount, it still prepares `_nextState`, but it does not queue a render or a callback. After mount, it appends the callback to `_stateCallbacks` and enqueues the component for rerendering.

### `forceUpdate(callback)`

`forceUpdate` schedules a rerender without changing state. It marks the component with `COMPONENT_FORCE`, which lets the renderer skip `shouldComponentUpdate` for that pass. Like `setState`, it only queues work once the component has mounted, and it stores the callback in `_renderCallbacks`.

### `render(props, state, context)`

`BaseComponent.prototype.render` defaults to `Fragment`. A subclass that omits `render()` therefore acts like a transparent wrapper: it returns its children and renders nothing when it has no output of its own.

## DOM and rerender helpers

### `getDomSibling(vnode, childIndex)`

`getDomSibling` finds the next rendered DOM node after a vnode.

- When `childIndex` is `null`, it resumes the search from the vnode's sibling in the parent tree.
- Otherwise, it scans the vnode's children until it finds the first child with a rendered `_dom`.
- If no child produces DOM and the vnode represents a function component, the search climbs through that wrapper and continues from there.

This logic lets the renderer find the correct insertion point even when the vnode tree contains function component wrappers or empty branches.

### `renderComponent(component)`

`renderComponent` rerenders a mounted component in place.

1. It copies the current vnode and bumps the copy's `_original` marker.
2. It diffs the copy against the live vnode inside the parent DOM container.
3. It commits refs and lifecycle work after the diff completes.
4. It replaces the old vnode in the parent tree with the new one.
5. It clears the old vnode's parent and DOM pointers.

When the rerender changes the root DOM node, `renderComponent` calls `updateParentDomPointers` so ancestor component vnodes keep a correct `_dom` reference.

### `updateParentDomPointers(vnode)`

`updateParentDomPointers` walks upward through parent component vnodes and refreshes each `_dom` pointer from the first rendered child. That repair keeps later sibling lookups and diffs aligned with the DOM that now exists.

## Scheduling and queue processing

### `rerenderQueue`

`rerenderQueue` stores dirty components that wait for the next flush.

### `enqueueRender(c)`

`enqueueRender` adds a component to the queue once per cycle.

- It sets the dirty bit before pushing.
- It avoids duplicate entries for the same component.
- It schedules `process()` through `options.debounceRendering` when that hook exists.
- It falls back to `queueMicrotask(process)` when no custom scheduler exists.

The scheduler also tracks the active debounce function, so a changed `options.debounceRendering` hook triggers a fresh flush.

### `depthSort(a, b)`

`depthSort` orders queued components by `_vnode._depth`. That keeps shallower components ahead of deeper descendants during a shared flush.

### `process()`

`process()` drains the queue and rerenders each dirty component in depth order.

- It keeps the queue sorted before it removes the next component.
- It skips entries whose dirty bit already cleared.
- It rerenders each remaining dirty component through `renderComponent()`.

A `finally` block clears `rerenderQueue` and resets `rerenderCount` after every flush. That reset matters when a render throws, because it keeps later updates schedulable.

### `resetRenderCount()`

`resetRenderCount()` sets the internal render counter back to `0`. The scheduler uses that counter to decide whether it needs to queue another flush.

## Reference

- `src/index.js` exposes `BaseComponent` as `Component`.
- `test/browser/components.test.jsx` covers mounted only scheduling, callback timing, depth ordered rerenders, and queue recovery after an error.