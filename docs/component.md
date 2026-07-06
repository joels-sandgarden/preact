# `src/component.js`

## Overview

This module drives component state changes, rerender scheduling, DOM sibling lookup, and pointer maintenance for the component system.

## Exports

### `BaseComponent`

`BaseComponent` stores `props`, `context`, and the internal state bits used by the component runtime. It also provides the component methods that drive updates:

- `setState()` merges state changes and schedules a rerender when the component is mounted.
- `forceUpdate()` marks the component for a forced render and queues it for rendering.
- `render()` supplies the default render implementation.

### Render helpers

The module exports the helpers that support component rendering and pointer maintenance:

- `renderComponent()` performs the diff and commit work for an updated component, then refreshes the vnode and DOM references.
- `updateParentDomPointers()` keeps parent `_dom` references in sync after updates.
- `getDomSibling()` walks vnode children and parent links to find the next DOM sibling.

### Scheduling helpers

The module also exports the rerender queue machinery:

- `enqueueRender()` adds mounted components to the rerender queue.
- `process()` drains the queue in depth order and runs component updates in batches.
- `resetRenderCount()` clears the batch counter that guards rerender work.

## `BaseComponent` behavior

`setState()` accepts either a partial state object or an updater function. It clones the current state, merges the result into the next state, and leaves the component marked for another render when the instance already mounts.

`forceUpdate()` sets the force render flag and places the component in the rerender queue even when state does not change.

`render()` gives subclasses a default implementation that returns `null` until a component supplies its own render logic.

## Render and update flow

1. A state change starts when `setState()` or `forceUpdate()` sets the component state flags.
2. `enqueueRender()` places the mounted component into the rerender queue.
3. `process()` groups queued work, sorts it by depth, and runs each update in batch order.
4. `renderComponent()` diffs the new vnode tree against the current output and commits the DOM changes.
5. `updateParentDomPointers()` restores the parent `_dom` references so later updates can find the correct insertion points.
6. `getDomSibling()` uses the vnode tree to locate the next DOM sibling whenever the renderer needs a stable reference.

## Update lifecycle summary

The update flow runs from state change to enqueueing, then through batched processing, diff and commit work, and finally pointer cleanup. That sequence keeps component updates predictable while the rerender queue limits redundant work and preserves DOM order.