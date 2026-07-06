# `src/component.js`

## Overview

`src/component.js` defines the internal component base constructor and the rerender path that keeps component state, DOM pointers, and update order aligned. The module focuses on how the renderer updates a component, not on public component authoring.

## BaseComponent

`BaseComponent` stores `props`, `context`, and `_bits`.

`setState()`:

- Reuses `_nextState` when a pending copy already exists.
- Clones `state` the first time it builds `_nextState`.
- Accepts a function and calls it with a cloned state object and `props`.
- Merges the returned partial state with `assign`.
- Pushes a completion callback into `_stateCallbacks`.
- Calls `enqueueRender()` only after the component has mounted and `_vnode` exists.

`forceUpdate()`:

- Sets `COMPONENT_FORCE` in `_bits`.
- Queues an optional callback in `_renderCallbacks`.
- Enqueues a rerender without going through `shouldComponentUpdate`.

`render` defaults to `Fragment`, so subclasses override it when they supply their own view.

## DOM sibling lookup and commit flow

`getDomSibling()`:

- Uses `NULL` as a sentinel when the search needs to resume from a vnode's sibling.
- Scans child vnodes until it finds the first child with a real `_dom` pointer.
- Walks through function component boundaries until it finds the next rendered DOM node.

`renderComponent()`:

- Clones the old vnode and bumps `_original`.
- Calls `diff()` with the old vnode, current context, hydrate state, and the next DOM sibling when needed.
- Calls `commitRoot()` after diffing.
- Replaces the old vnode in the parent child array with the updated vnode.
- Clears the old vnode's `_parent` and `_dom` pointers.
- Calls `updateParentDomPointers()` when the committed DOM node changes.

`updateParentDomPointers()` repairs ancestor `_dom` pointers by taking the first rendered child it can find, so later sibling lookups keep the right insertion point.

## Render queue and batching

`enqueueRender()` marks the component dirty, adds it to `rerenderQueue`, and schedules `process()` with `options.debounceRendering` or `queueMicrotask()` when no custom scheduler exists.

`process()` sorts queued components by vnode depth, flushes them in parent before child order, keeps new items in the same pass, and uses `try/finally` to clear `rerenderQueue` and `rerenderCount` after every run, even when rendering throws.

`resetRenderCount()` clears the rerender counter when the caller needs to restart the flush guard.