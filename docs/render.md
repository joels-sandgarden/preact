# `src/render.js` Reference

## Overview

This page documents the `src/render.js` module only. The module exports `render(vnode, parentDom)` and `hydrate(vnode, parentDom)`.

```js
render(vnode, parentDom)
hydrate(vnode, parentDom)
```

## Prerequisites

- A virtual node.
- A DOM container.

## `render(vnode, parentDom)`

`render()` updates a DOM container from a virtual node.

1. It switches `document` to `document.documentElement` so the root target always points to an element.
2. It calls `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags & MODE_HYDRATE` to decide whether the call runs in hydration mode.
4. It reads `parentDom._children` for the previous tree unless hydration mode skips that lookup.
5. It stores `createElement(Fragment, NULL, [vnode])` on `parentDom._children`.
6. It calls `diff()` with the stored tree, the existing DOM children on a first render, the namespace, the hydration flag, and `parentDom.ownerDocument`.
7. It calls `commitRoot(commitQueue, parentDom._children, refQueue)` after diffing finishes.

## `hydrate(vnode, parentDom)`

`hydrate()` marks the vnode for hydration and then delegates to `render()`.

1. It sets `MODE_HYDRATE` on the vnode.
2. It calls `render(vnode, parentDom)`.

## Runtime details

- `parentDom._children` stores the latest vnode tree for repeat renders on the same container.
- Hydration mode skips the previous tree lookup and lets `diff()` work against the existing DOM.
- First renders pass `parentDom.firstChild ? slice.call(parentDom.childNodes) : NULL` into `diff()` so the renderer can reconcile existing nodes.
- `commitRoot()` flushes the commit queue and the ref queue after diffing completes.

## Reference

- `render(vnode, parentDom)` renders a vnode into a DOM container.
- `hydrate(vnode, parentDom)` marks a vnode for hydration and renders it into a DOM container.