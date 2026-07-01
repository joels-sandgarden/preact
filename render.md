# `src/render.js` Reference

## Overview

`src/render.js` provides the runtime entry point that reconciles a vnode tree into a DOM container. Preact's runtime uses diffing-based DOM reconciliation, and this module starts that process for both fresh renders and hydration.

## Public exports

- `render(vnode, parentDom)`: Reconciles `vnode` into `parentDom`.
- `hydrate(vnode, parentDom)`: Sets `MODE_HYDRATE` on `vnode` and calls `render()`.

The package entry point re-exports both functions from `src/render.js`.

## Render flow

1. `render()` normalizes `document` to `document.documentElement` when `parentDom` equals `document`.
2. It calls `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags & MODE_HYDRATE` to determine hydration mode.
4. It reads `parentDom._children` as the previous vnode tree unless hydration is active.
5. It wraps `vnode` in `Fragment` and stores the wrapper on `parentDom._children`.
6. It prepares `commitQueue` and `refQueue`, then calls `diff()` with the current tree, the previous tree, the DOM siblings, and the hydration state.
7. It calls `commitRoot()` to flush the queued effects and refs.

## Hydration entry point

`hydrate()` sets the `MODE_HYDRATE` flag on `vnode` and delegates to `render()`. 