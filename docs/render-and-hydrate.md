# Render and Hydrate

## Overview

This document covers `src/render.js`, the module that turns a vnode tree into DOM and updates the same container on later calls.

## `render(vnode, parentDom)`

`render` handles the full vnode to DOM flow.

1. It normalizes `document` containers to `document.documentElement`.
2. It runs `options._root(vnode, parentDom)` when that hook exists.
3. It checks `vnode._flags` for `MODE_HYDRATE` to decide whether the call hydrates or renders normally.
4. It reads `parentDom._children` as the previous tree when the call does not hydrate.
5. It stores `createElement(Fragment, null, [vnode])` back on `parentDom._children` so the next call can compare against the last tree.
6. It creates `commitQueue` and `refQueue`, then calls `diff(...)` with the current vnode tree, the previous tree, the current DOM children, and the hydration flag.
7. It calls `commitRoot(commitQueue, parentDom._children, refQueue)` to flush refs and queued callbacks after the diff completes.

## `hydrate(vnode, parentDom)`

`hydrate` stays thin.

1. It sets `MODE_HYDRATE` on `vnode._flags`.
2. It calls `render(vnode, parentDom)` immediately.

Hydration does not use a separate renderer. It follows the render path with a hydration flag that tells the diff step to reconcile against existing DOM instead of starting from a clean mount.

## Render vs. hydration

Normal render and hydration use the same reconciliation flow, but they start from different assumptions.

- Normal render reuses `parentDom._children` as the previous tree and lets the diff step update the container from that cached vnode tree.
- Hydration sets `MODE_HYDRATE` so the diff step attaches to existing DOM and checks what is already in the container.
- Both paths end in `diff(...)` and `commitRoot(...)`.

## Related flags

`MODE_HYDRATE` marks a vnode for hydration, and `RESET_MODE` clears mode bits after a successful diff pass.
