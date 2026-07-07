# `src/component.js`

## Overview

`src/component.js` defines the core component runtime for the renderer. It gives components shared state update helpers, DOM sibling lookup, rerender handling, and queue processing.

## Base component API

### `BaseComponent(props, context)`

The constructor stores `props`, `context`, and `_bits` on each component instance.

### `setState(update, callback)`

`setState()` merges a partial update into pending state:

- The first update clones `state` into `_nextState`.
- Function updates receive a cloned copy of the pending state and the current props.
- Falsy updates return without changing state.
- When the component has a vnode, it queues `callback` in `_stateCallbacks` and schedules the component with `enqueueRender()`.

### `forceUpdate(callback)`

`forceUpdate()` sets the `COMPONENT_FORCE` flag, queues `callback` in `_renderCallbacks`, and schedules the component. This flag lets the update path skip `shouldComponentUpdate`.

### `render(props, state, context)`

The default implementation points to `Fragment`, so components that do not override `render()` return a fragment.

## DOM lookup and rerendering

### `getDomSibling(vnode, childIndex)`

`getDomSibling()` finds the next rendered DOM node for a vnode. It resumes from the parent when no child index is supplied, scans child vnodes for the first one with `_dom`, and falls back to the next sibling for function components.

### `renderComponent(component)`

`renderComponent()` rerenders a component in place. It clones the current vnode, diffs the clone against the previous vnode, commits queued DOM and ref work, clears stale parent links, and refreshes parent DOM pointers when the rendered DOM node changes.

### `updateParentDomPointers(vnode)`

`updateParentDomPointers()` walks up through parent components and rebuilds each ancestor `_dom` pointer from the first child that still has a rendered DOM node.

## Render queue and scheduler

### `enqueueRender(c)`

`enqueueRender()` marks a component dirty, adds it to the rerender queue once, and schedules `process()` with `options.debounceRendering` or `queueMicrotask()`.

### `resetRenderCount()`

`resetRenderCount()` clears the scheduler guard counter so future work can schedule a new flush.

### `process()`

`process()` flushes the queue. It keeps the queue sorted by component depth, rerenders dirty components with `renderComponent()`, and clears the queue in a `finally` block.

### `depthSort`

`depthSort` orders components by `_vnode._depth` so parent components render before child components.