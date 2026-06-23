# Core Runtime Reference

## Overview

This document describes the runtime path that turns vnodes into DOM, batches component updates, and handles context, cloning, hooks, and errors.

## Runtime map

| Concept | Source files | What the runtime does |
| --- | --- | --- |
| Vnode creation | `src/create-element.js`, `jsx-runtime/src/index.js` | Builds normalized vnodes from `createElement`, `Fragment`, and JSX runtime calls. |
| Render and hydrate | `src/render.js` | Reconciles a vnode tree into a parent DOM node and enables hydration mode. |
| Diffing and child reconciliation | `src/diff/index.js`, `src/diff/children.js` | Compares new and stored trees, reuses DOM when possible, and keeps child order stable. |
| Component model and render queue | `src/component.js` | Provides state updates, forced updates, queueing, and ordered flushes. |
| Context propagation | `src/create-context.js` | Publishes context values, tracks subscribers, and updates consumers when the value changes. |
| Cloning | `src/clone-element.js` | Copies a vnode, merges props, and replaces key, ref, or children when needed. |
| Options hooks | `src/options.js` | Exposes renderer hooks for add-ons and integration packages. |
| Constants and flags | `src/constants.js` | Defines mode bits, component bits, namespace values, and shared sentinels. |
| Error handling | `src/diff/catch-error.js` | Walks the vnode chain, invokes error boundaries, and preserves recovery state. |

## Vnode creation

The classic factory in `src/create-element.js` and the automatic JSX runtime in `jsx-runtime/src/index.js` both create normalized vnode objects. They copy props, preserve keys and refs, attach internal bookkeeping fields, and run vnode hooks when a vnode enters the tree for the first time.

## Render and hydrate

`render` stores the previous vnode tree on the parent DOM node, prepares commit and ref queues, and runs the diff against the new tree. `hydrate` marks the vnode tree for hydration before it calls `render`, so the diff can attach to existing markup instead of rebuilding it.

## Diffing and child reconciliation

The diff engine compares the new tree with the stored tree, reuses matching DOM, updates props, inserts or moves nodes, and removes leftovers. `src/diff/children.js` flattens child lists, matches keys and types, and keeps the DOM order stable while it walks each branch of the tree.

## Component model and render queue

`src/component.js` defines the component base class and the render queue that drives updates. `setState` merges the next state and queues a render, `forceUpdate` marks a component for an immediate refresh, and the queue sorts pending components by tree depth before it flushes them.

## Context propagation

`src/create-context.js` builds a provider and consumer pair around a shared context value. The provider stores the current value in child context, tracks subscribers, and marks them dirty when the value changes so dependent components refresh together.

## Cloning

`src/clone-element.js` creates a new vnode from an existing vnode. It copies the original props, applies any new props, and replaces the key, ref, or children when the caller supplies new values.

## Options hooks

`src/options.js` exposes the hook surface that add-ons and renderer packages use to observe runtime events. The runtime calls those hooks around vnode creation, diffing, rendering, commit work, and error handling.

## Constants and flags

`src/constants.js` defines the mode bits and component bits that the runtime uses to track hydration, forced updates, dirty components, and pending errors. It also provides namespace values and shared sentinel values that keep the diff path consistent across SVG, XHTML, and MathML content.

## Error handling

`src/diff/catch-error.js` walks up the vnode chain until it finds an error boundary. It calls `getDerivedStateFromError` or `componentDidCatch`, marks the boundary with pending error state when it handles the failure, resets the render counter, and rethrows the error when no boundary can recover.

## Related pages

- [Overview](./overview.md)
- [Packages](./packages.md)
- [Development workflow](./development.md)