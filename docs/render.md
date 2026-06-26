# `src/render.js` Reference

## Overview

This document describes the `src/render.js` module. It covers the public `render()` and `hydrate()` exports and the runtime steps they use to update the DOM.

## Prerequisites

- Familiarity with Preact virtual nodes and DOM containers.
- A DOM target for the render call.

## `render(vnode, parentDom)`

`render()` accepts a virtual node and a DOM container.

1. It switches `document` to `document.documentElement` so the root target always points to an element.
2. It calls `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags & MODE_HYDRATE` to decide whether the call runs in hydration mode.
4. It reads the previous tree from `parentDom._children` unless hydration mode skips that value.
5. It stores the new tree on `parentDom._children` as a `Fragment` that wraps the supplied vnode.
6. It calls `diff()` with the current DOM state, the previous vnode tree, the hydration flag, and the document owner.
7. It flushes queued work with `commitRoot()` after diffing finishes.

## `hydrate(vnode, parentDom)`

`hydrate()` prepares the vnode for hydration and then delegates to `render()`.

1. It sets `MODE_HYDRATE` on the vnode.
2. It calls `render(vnode, parentDom)`.

## Runtime details

- `parentDom._children` keeps the latest vnode tree for repeated renders on the same container.
- Hydration mode tells `render()` to ignore the stored tree and work from the existing DOM.
- `diff()` receives the DOM children that already exist in the container when the module mounts into a node for the first time.
- `commitRoot()` flushes the commit queue and the ref queue after diffing completes.

## Reference

- `render(vnode, parentDom)` renders a vnode into a DOM container.
- `hydrate(vnode, parentDom)` marks a vnode for hydration and renders it into a DOM container.