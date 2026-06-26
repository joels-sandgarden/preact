# Render Module

## Overview

`src/render.js` exposes the public entry points for rendering and hydration.

## Prerequisites

- Familiarity with vnodes and DOM containers.

## `render()`

`render()` accepts a vnode and a parent DOM node. It then:

1. Uses the existing root vnode when `parentDom._children` already points at one.
2. Reconciles the new vnode against the current DOM state through diffing.
3. Applies hydration rules when the vnode arrives in hydration mode.
4. Runs root hooks after diffing completes.
5. Flushes the ref and commit queues so DOM side effects land after the tree settles.

The function also stores the reconciled root vnode in `parentDom._children`. That cache lets later renders compare against the last rendered tree.

## `hydrate()`

`hydrate()` prepares a vnode for hydration, then calls `render()` with the same parent DOM node. It gives `render()` the signal it needs to match the vnode against existing DOM instead of building a fresh tree from scratch.

## Hydration and commit flow

Hydration starts by treating the existing DOM as the source of truth. `render()` then matches the vnode to that DOM, updates the root vnode cache, and hands control to the diffing process. After diffing finishes, root hooks run, and the ref and commit queues flush in order. That sequence keeps DOM updates, refs, and post render effects in sync with the final tree.