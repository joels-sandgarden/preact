# `preact/debug`

## Overview

The `preact/debug` entry point initializes debug instrumentation and loads `preact/devtools` when a project imports it. It exposes development-only helpers for component stack tracing, display name lookup, and repeated prop warning resets.

## Helpers

- `captureOwnerStack()` returns the component stack that the debug runtime has captured so far.
- `getCurrentVNode()` returns the currently rendered `VNode`, or `null` when no render is active.
- `getDisplayName(vnode)` returns a readable name for a component or DOM node.
- `getOwnerStack(vnode)` returns the component stack for the given `VNode`.
- `setupComponentStack()` prepares the runtime to capture component traces during rendering.
- `resetPropWarnings()` clears the recorded prop warning history so repeated warnings can log again.

## Example

```js
import { captureOwnerStack, setupComponentStack } from 'preact/debug';

setupComponentStack();

const stack = captureOwnerStack();
console.log(stack);
```

## When to reset warnings

Call `resetPropWarnings()` before another diagnostic pass when the same prop warning needs to appear again. The helper clears the stored warning state so the next render can log it again.