# `src/render.js` Reference

## Overview

`src/render.js` is the runtime entry point for reconciling a vnode tree into a DOM container. Preact's runtime uses diffing-based DOM reconciliation, and this module starts that work for both render and hydration.

## Public exports

- `render(vnode, parentDom)`: Reconciles `vnode` into `parentDom`.
- `hydrate(vnode, parentDom)`: Sets `MODE_HYDRATE` on `vnode` and calls `render()`.

The package entry point in `src/index.js` re-exports both functions.

## Render flow

1. `render()` normalizes `document` to `document.documentElement` when `parentDom` equals `document`.
2. It calls `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags & MODE_HYDRATE` to detect hydration.
4. It reads `parentDom._children` as the previous vnode tree unless hydration is active.
5. It wraps `vnode` in `Fragment` and stores the wrapper on `parentDom._children`.
6. It prepares `commitQueue` and `refQueue`, then calls `diff()` with the new tree, the previous tree, the current DOM node list, and the hydration state.
7. It calls `commitRoot()` to flush the queued effects and refs.

## Hydration

`hydrate()` sets the `MODE_HYDRATE` flag on `vnode` and delegates to `render()`.