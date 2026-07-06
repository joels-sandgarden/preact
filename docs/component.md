# Base Component and Rendering Pipeline

## Overview

This document describes `BaseComponent` in `src/component.js` and the helpers that keep component updates, rerender scheduling, and DOM placement in sync. See the repository overview in [README](../README.md) for broader project context. It covers `setState()`, `forceUpdate()`, the default `render()` method, and the functions that locate sibling DOM nodes and flush the render queue.

## Prerequisites

- Familiarity with component props, state, and context.
- Basic knowledge of virtual DOM rendering.

## Implementation

### `BaseComponent`

`BaseComponent` stores the initial `props`, the initial `context`, and the internal render flags used by the update queue. It gives each component the public `setState()` and `forceUpdate()` methods.

### `setState()`

`setState()` clones the pending state on first use, then merges the next partial state into that copy.

- It accepts either an object or a function.
- When it receives a function, it calls that function with a copy of the current state and the current props.
- It ignores empty updates and returns without scheduling work.
- When the component already has a mounted vnode, it queues the component for rerender.
- When a callback exists, it stores the callback so the callback can run after the state update completes.

### `forceUpdate()`

`forceUpdate()` queues an immediate rerender for a mounted component.

- It marks the component so the render path skips `shouldComponentUpdate`.
- It stores an optional callback for the post render phase.
- It queues the component through the same scheduler that `setState()` uses.

### `render()`

`BaseComponent.prototype.render` points to `Fragment`. The default implementation gives the base class a fragment render path until a subclass defines its own `render()` method. That default produces no standalone UI of its own.

### DOM and scheduling helpers

#### `getDomSibling()`

`getDomSibling()` finds the next rendered DOM node after a vnode.

- It resumes the search from the current vnode's children when a child index exists.
- It walks up to parent vnodes when the current subtree does not contain a rendered node.
- It returns `NULL` when no later DOM node exists.

#### `renderComponent()`

`renderComponent()` rerenders a mounted component against its parent DOM node.

- It copies the current vnode before the diff starts.
- It runs the diff against the current parent DOM node and context.
- It commits refs and queued side effects after the diff completes.
- It replaces the old vnode with the new vnode and refreshes parent DOM pointers when the rendered DOM node changes.

#### `updateParentDomPointers()`

`updateParentDomPointers()` walks up through parent component vnodes and refreshes their cached DOM pointers.

- It clears the cached DOM reference on each parent component vnode.
- It stores the first rendered child DOM node it finds.
- It keeps sibling lookup aligned with the current rendered tree.

#### `enqueueRender()`, `process()`, and `resetRenderCount()`

- `enqueueRender()` marks a component dirty, adds it to the render queue, and schedules processing through `options.debounceRendering()` when that hook exists or `queueMicrotask()` otherwise.
- `process()` sorts the queue by component depth, rerenders dirty components from top to bottom, and clears the queue at the end of the pass.
- `resetRenderCount()` clears the counter that limits repeated scheduling.

## Code Examples

```js
import { BaseComponent } from '../src/component.js';

class Counter extends BaseComponent {
  constructor(props, context) {
    super(props, context);
    this.state = { count: 0 };
  }

  render(props, state) {
    return state.count;
  }

  increment() {
    this.setState(prev => ({ count: prev.count + 1 }));
  }

  refresh() {
    this.forceUpdate();
  }
}
```

This example shows `setState()` and `forceUpdate()` on a subclass that defines its own render path.

## Best Practices

- Keep state updates small so rerenders touch only the data that changed.
- Use `setState()` for normal updates and `forceUpdate()` only when the render path needs to run again without a state change.
- Return a new partial state from function updates so the scheduler can merge the result predictably.
- Override `render()` in every subclass that needs visible output.

## Troubleshooting

### A state update does not trigger a rerender

Confirm that the component has mounted. `setState()` queues work only after the component receives a vnode.

### `forceUpdate()` has no effect

Confirm that the component is still mounted. The method exits early when the component does not have a vnode.

### DOM placement changes after a rerender

Use `getDomSibling()` and `updateParentDomPointers()` together with the diff process. These helpers keep the next insertion point aligned with the current rendered tree.

## Reference

- [Repository overview](../README.md)
- [`src/component.js`](../src/component.js)