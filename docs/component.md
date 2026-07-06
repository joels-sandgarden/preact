# `src/component.js`

## Overview

This module runs the component update layer for the runtime. It defines shared base component behavior, queues rerenders, and sends component updates through the same diff and commit path that root `render()` calls use.

## Exports

### Public surface

- `BaseComponent` supplies the shared constructor for class components and function components.
- `setState()` clones state, merges partial updates, stores callbacks, and schedules a rerender once mounted.
- `forceUpdate()` marks a component for a forced render and skips `shouldComponentUpdate()`.
- `render()` points to `Fragment` by default, so a component without its own render method renders through the fragment path.

`src/index.js` re-exports `BaseComponent` as `Component`, so the package entry point exposes the same base type under the familiar name.

### Internal helpers

The runtime calls these helpers directly, but the module keeps them private:

- `getDomSibling()` finds the next mounted DOM node after a vnode.
- `renderComponent()` reruns diffing for an existing component vnode and commits the result.
- `updateParentDomPointers()` refreshes ancestor `_dom` pointers after a move or replacement.
- `enqueueRender()` marks a component dirty, adds it to the render queue, and schedules `process()`.
- `process()` drains the render queue in depth order.
- `resetRenderCount()` clears the internal scheduling guard used by the queue.

## State updates

`setState()` clones the current state into `_nextState` the first time it runs, then merges the partial update into that copy. When the update argument is a function, it receives a cloned snapshot of the current state and the current props, and it can return the partial state to merge.

If `setState()` receives a callback, the method stores that callback in `_stateCallbacks`. `renderComponent()` passes those callbacks to `commitRoot()`, which runs them after refs and lifecycle work finish. The method only enqueues work once the component already has a vnode, so constructor calls do not schedule a render.

`forceUpdate()` sets `COMPONENT_FORCE` on the instance, stores any callback in `_renderCallbacks`, and enqueues a rerender. The next update bypasses `shouldComponentUpdate()`.

`COMPONENT_DIRTY` marks queued components, `COMPONENT_FORCE` marks forced updates, and `MODE_HYDRATE` keeps hydration work on the same update path when a vnode renders during hydration.

## Render pipeline

`renderComponent()` bridges an existing component instance back into the shared diff pipeline. It clones the current vnode, bumps the clone's original marker, diffs the clone against the old vnode, stores the new vnode, and calls `commitRoot()` with the collected ref and lifecycle queues.

`src/render.js` follows the same pattern for root renders: it creates a vnode tree, calls `diff()`, and finishes with `commitRoot()`. Component updates therefore follow the same commit order as an initial render.

`commitRoot()` flushes refs first and then runs queued component callbacks. `setState()` and `forceUpdate()` both rely on that order when they collect lifecycle work.

`updateParentDomPointers()` keeps ancestor `_dom` references accurate after a child moves or the rendered DOM node changes. It clears each ancestor component's stored DOM anchor and rebuilds it from the first live child DOM node it finds.

## DOM sibling lookup

`getDomSibling()` finds the next mounted DOM node for insertions and replacements. When it starts from a vnode child index, it scans the remaining children until it finds a vnode with a live `_dom` pointer. When a subtree has no direct DOM sibling, the helper climbs through parent component vnodes and continues the search from the next sibling in the parent array.

The tests cover the cases that matter here: direct siblings, text nodes, fragments, placeholders, nested components, wrapper components that return JSX children, and empty subtrees that must return `null`.

## Render queue

`enqueueRender()` marks a component dirty, pushes it onto the rerender queue once, and schedules `process()` with `options.debounceRendering` when that hook exists. If no custom debouncer exists, the module falls back to `queueMicrotask()`.

`process()` drains the queue in depth order so parent updates run before deeper descendants. New renders can join the queue during a flush, and `process()` sorts again before it continues so parents still run before deeper descendants. That behavior matters when a parent update adds work for children while the queue still runs.

`resetRenderCount()` exists as an internal helper for queue recovery and tests. It resets the guard that prevents duplicate scheduling while the queue drains.
