# `src/component.js`

## Overview

`src/component.js` defines the base component runtime and the internal render queue used by the renderer.

## Base component API

### `BaseComponent(props, context)`

The constructor stores `props`, `context`, and `_bits` on the component instance.

### `setState(update, callback)`

`setState()` merges a partial update into pending state:

- The first update clones `state` into `_nextState`.
- Function updates receive a cloned copy of the pending state and the current props.
- Falsy updates return without changing state.
- When the component already has a vnode, it queues `callback` in `_stateCallbacks` and schedules the component with `enqueueRender()`.

### `forceUpdate(callback)`

`forceUpdate()` sets the `COMPONENT_FORCE` flag, queues `callback` in `_renderCallbacks`, and schedules the component. The update path uses this flag to skip `shouldComponentUpdate`.

### `render(props, state, context)`

The default implementation returns `Fragment`, so components that do not override `render()` render a fragment.

## DOM lookup and rerendering

### `getDomSibling(vnode, childIndex)`

`getDomSibling()` finds the next rendered DOM node for a vnode. When `childIndex` is `null`, it resumes from the parent sibling. Otherwise it scans child vnodes for the first one with `_dom`, then falls back to the next sibling for function components.

### `renderComponent(component)`

`renderComponent()` rerenders a component in place. It clones the current vnode, diffs the clone against the previous vnode, commits queued DOM and ref work, clears stale parent links, and refreshes parent DOM pointers when the rendered DOM node changes.

### `updateParentDomPointers(vnode)`

`updateParentDomPointers()` walks up through parent components and rebuilds each ancestor `_dom` pointer from the first child that still has rendered DOM.

## Render queue and scheduler

### `enqueueRender(c)`

`enqueueRender()` marks a component dirty, adds it to the rerender queue once, and schedules `process()` with `options.debounceRendering` or `queueMicrotask()`.

### `resetRenderCount()`

`resetRenderCount()` clears the scheduler guard counter so later work can schedule a new flush.

### `process()`

`process()` flushes the queue. It sorts queued components by depth when needed, rerenders dirty components with `renderComponent()`, and clears the queue in a `finally` block.

### `depthSort`

`depthSort` orders components by `_vnode._depth` so parent components render before child components.