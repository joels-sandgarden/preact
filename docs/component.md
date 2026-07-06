# Component reference

## Overview

The component module powers Preact's class component base class and the queue that drives mounted component updates. The public `Component` export maps to `BaseComponent`, so application code reaches this behavior through the public API.

## API summary

- `BaseComponent(props, context)`: creates a component instance and stores `props`, `context`, and update bookkeeping.
- `getDomSibling(vnode, childIndex?)`: finds the next rendered DOM node after a vnode.
- `resetRenderCount()`: clears the queue flush counter used by the render scheduler.
- `enqueueRender(component)`: marks a mounted component dirty and schedules a queue flush.

## Component state and update bookkeeping

`BaseComponent` keeps its pending work in internal fields:

- `_bits` stores update flags such as `COMPONENT_FORCE` and `COMPONENT_DIRTY`.
- `_nextState` holds the next state object before render runs.
- `_renderCallbacks` stores callbacks that run after render.
- `_stateCallbacks` stores callbacks passed to `setState`.
- `_vnode` points to the current vnode.
- `_parentDom` points to the parent DOM node for in place rerenders.

`setState()` merges partial state into `_nextState`. It also accepts an updater function, and that function receives a copy of the pending state plus the current `props`. When the component is already mounted, `setState()` stores the callback in `_stateCallbacks` and calls `enqueueRender()`.

`forceUpdate()` sets `COMPONENT_FORCE`, stores any callback in `_renderCallbacks`, and enqueues the component. The next render skips `shouldComponentUpdate()` because the force bit stays set until the update runs. `BaseComponent.prototype.render` points to `Fragment`, so subclasses override `render()` with their own output.

## DOM sibling lookup

`getDomSibling()` locates the next rendered DOM node after a vnode. It scans the vnode's children from the requested index, skips empty branches, and returns the first child with a live `_dom` pointer. When a vnode has no rendered child of its own, the helper climbs to the parent vnode and resumes the search there. It returns `null` when it reaches the end of the rendered tree.

## Render queue

`enqueueRender()` marks a component dirty with `COMPONENT_DIRTY`, adds it to the rerender queue, and schedules `process()`. The render queue flush runs on `queueMicrotask()` by default, or through `options.debounceRendering` when that hook exists.

`process()` drains the queue in depth order. `depthSort()` sorts queued components by vnode depth so parent updates run before nested updates. `process()` keeps consuming the queue until it empties, which lets new updates that appear during a flush join the same pass.

`renderComponent()` performs the in place rerender. It clones the current vnode, runs `diff()` against the previous tree, commits the changes with `commitRoot()`, and then refreshes cached parent DOM pointers with `updateParentDomPointers()` when the rendered DOM node changes. This pipeline keeps the component tree and DOM tree aligned while class component updates move through the queue.

## Reference

`getDomSibling()` and the rerender pipeline both depend on the vnode tree staying current, especially when fragments, placeholders, or nested components leave no direct DOM child behind.