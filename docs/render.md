# `src/render.js` Reference

## Overview

This page covers the `src/render.js` module only. The module exports `render(vnode, parentDom)` and `hydrate(vnode, parentDom)`.

```js
render(vnode, parentDom)
hydrate(vnode, parentDom)
```

## Prerequisites

- A virtual node.
- A DOM container.

## `render(vnode, parentDom)`

`render()` updates a DOM container from a virtual node.

1. When the caller passes `document`, it switches the target to `document.documentElement`.
2. It calls `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags & MODE_HYDRATE` to decide whether the call runs in hydration mode.
4. It reads `parentDom._children` for the previous tree when `MODE_HYDRATE` is not set.
5. It stores `createElement(Fragment, NULL, [vnode])` on `parentDom._children`.
6. It calls `diff()` with the stored tree, the namespace, the hydration flag, `parentDom.ownerDocument`, and either the previous vnode tree or the current DOM children when `parentDom._children` does not exist.
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
