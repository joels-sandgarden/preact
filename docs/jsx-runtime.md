# Automatic JSX Runtime

## Overview

This document describes the automatic JSX runtime exported by `preact/jsx-runtime`.
`preact/jsx-dev-runtime` exposes the same API surface and adds the development entry point expected by JSX tooling.

Note: production builds use `preact/jsx-runtime`, and development builds use `preact/jsx-dev-runtime`.

## Prerequisites

- A JSX transform that targets the automatic runtime.
- `preact` installed in the project.
- A build setup that routes JSX output to `preact`.

## Configuration

1. Configure the JSX transform to use the automatic runtime and `preact` as the import source.
2. Verify that compiled JSX output imports from `preact/jsx-runtime` in production builds and `preact/jsx-dev-runtime` in development builds.

```json
{
  "plugins": [
    ["@babel/plugin-transform-react-jsx", { "runtime": "automatic", "importSource": "preact" }]
  ]
}
```

## Helper reference

### `jsx`, `jsxs`, and `jsxDEV`

`jsx`, `jsxs`, and `jsxDEV` all create vnodes from a component or intrinsic element, a props object, and an optional key.
The runtime uses the same vnode creation path for all three helpers.

- `jsx` handles the standard automatic runtime output.
- `jsxs` handles output that includes multiple static children.
- `jsxDEV` handles development output and carries source information for debugging.

The runtime normalizes `ref` before it stores props on the vnode.
When the type is not a function and the props include `ref`, it copies the props, removes `ref` from the vnode props, and stores the reference on the vnode itself.
After the vnode exists, the runtime calls `options.vnode(vnode)` when the hook is present.

### `Fragment`

`Fragment` lets the runtime create fragment vnodes without adding an extra DOM element.

### `jsxTemplate`

`jsxTemplate` supports precompiled JSX transforms that emit a template string array and a list of expressions.
It builds a fragment vnode that carries the template data and the expression list.

### `jsxAttr`

`jsxAttr` serializes an attribute for precompiled output.
It ignores `ref` and `key`, gives hooks from `options.attr` the first chance to format the value, and converts style objects into CSS text before encoding the result.
It omits null, false, function, and object values that do not resolve to text, and it emits a bare attribute name for `true`.

### `jsxEscape`

`jsxEscape` prepares dynamic child content for template output.
It returns `null` for nullish values, booleans, and functions, preserves vnode objects, walks arrays recursively, and encodes primitive values as text.

### `JSX`

`JSX` exports the `JSXInternal` type alias for TypeScript consumers.
Use it for JSX type checking and intrinsic element typing.

## Code examples

### Automatic runtime configuration

```json
{
  "compilerOptions": {
    "jsx": "react-jsx",
    "jsxImportSource": "preact"
  }
}
```

```jsx
export function App() {
  return <h1>Hello from Preact</h1>;
}
```

The compiler adds the runtime imports automatically, so the source file stays focused on JSX.

### Precompiled template usage

```js
import { jsxTemplate, jsxAttr, jsxEscape } from 'preact/jsx-runtime';

const label = '<safe text>';
const href = '/docs?tab=runtime';

const vnode = jsxTemplate(
  ['<a href="', '">', '</a>'],
  jsxAttr('href', href),
  jsxEscape(label)
);
```

This pattern lets a precompiled transform serialize attributes and escape child content before render time.

## Compatibility aliases

`preact/compat/jsx-runtime` and `preact/compat/jsx-dev-runtime` load `preact/compat` and then re-export the same runtime helpers.
Use these entry points when a compatibility build expects the compat package name.