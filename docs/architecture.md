# Core Architecture

## Overview

`preact` centers on vnode creation, DOM reconciliation, and component updates.

## Rendering flow

- `createElement`, `h`, and the JSX runtime build vnodes from component trees.
- `render` and `hydrate` reconcile vnodes into a parent DOM node.
- The diff system compares the new tree with stored children and applies the smallest useful DOM changes.

## Component model

- `Component` provides state and update methods.
- `setState` queues work through the render scheduler.
- `forceUpdate` marks a component for an immediate refresh.

## Extension points

- `options` exposes hooks for add-ons and renderer callbacks.
- `preact/hooks`, `preact/debug`, `preact/compat`, and `preact/devtools` connect through those hooks.

## Related pages

- [Overview](./overview.md)
- [Packages](./packages.md)
- [Development workflow](./development.md)