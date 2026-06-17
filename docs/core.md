# Root `preact` API

## Overview

This page documents the root `preact` package. It covers the runtime API, the component model, context helpers, shared utilities, and the public types that support those exports.

The JSX intrinsic element map and the DOM and event typing live in the repository declaration files and do not repeat here.

## Rendering

### `render(vnode, parent)`

Use `render()` to mount a component tree into a container that matches `ContainerNode`. Later calls reuse the same mounted tree and update the existing DOM.

### `hydrate(vnode, parent)`

Use `hydrate()` when server rendered HTML already exists in the container. It attaches Preact to that DOM and continues with normal updates after the first pass.

### `ContainerNode`

`ContainerNode` describes the minimum container interface that `render()` and `hydrate()` need. The type includes child access and the DOM operations that Preact uses while it reconciles updates.

## Component creation

### `createElement()` and `h()`

`createElement()` and its alias `h()` build virtual nodes from an element name, a component, props, and children. The exported overloads preserve strong typing for standard HTML and SVG elements, custom elements, and component props.

### `Fragment`

`Fragment` lets a component return a group of children without adding an extra wrapper element.

### `cloneElement(vnode, props, ...children)`

Use `cloneElement()` to copy an existing virtual node, merge new props into it, and replace or extend its children. This helper keeps the original element type while applying the new values.

### `createRef()`

Use `createRef()` to create an object ref with a mutable `current` property. Attach that ref to a component instance or DOM node when a stable reference is needed.

### `isValidElement(vnode)`

Use `isValidElement()` to test whether a value is a Preact virtual node.

## Context

### `createContext(defaultValue)`

Use `createContext()` to define shared state for a subtree. The returned context object exposes both `Provider` and `Consumer` so components can share values without threading props through each level.

### `Provider` and `Consumer`

`Provider` accepts a `value` and an optional `children` tree. `Consumer` accepts a render function that receives the current context value and returns children.

### `Context` and `ContextType`

`Context<T>` describes the object returned by `createContext()`. `ContextType<C>` resolves the value type carried by a context object.

## Helpers

### `toChildArray(children)`

Use `toChildArray()` to flatten children into a predictable array that only contains renderable vnode, string, and number entries.

### `options`

`options` exposes global hooks for lifecycle, event handling, scheduling, debug values, suspense coordination, and attribute serialization.

- `vnode`: runs when Preact creates a vnode.
- `unmount`: runs just before Preact removes a vnode.
- `diffed`: runs after Preact finishes a vnode update.
- `event`: intercepts browser events before Preact handles them.
- `requestAnimationFrame` and `debounceRendering`: control render scheduling.
- `useDebugValue` and `_addHookName`: support debug tooling.
- `__suspenseDidResolve`: coordinates suspense resolution.
- `attr`: customizes attribute serialization for precompiled JSX.

## Component base class

### `Component`

Extend `Component` for stateful views that need lifecycle methods or explicit update control. The base class exposes `props`, `state`, `context`, `setState()`, and `forceUpdate()`.

`componentDidCatch(error, errorInfo)` receives an `ErrorInfo` object with an optional `componentStack` string. `contextType` connects a class to one context value.

## Type reference

### Core virtual node types

- `VNode<P>`: Describes a virtual node with `type`, `props`, `key`, and optional `ref`.
- `Key`: Represents child identity. It accepts string, number, or any comparable value that Preact can use.
- `ComponentChild`: Represents one child value. It includes virtual nodes, plain objects, strings, numbers, bigints, booleans, `null`, and `undefined`.
- `ComponentChildren`: Represents one child or an array of children.

### Ref types

- `RefObject<T>`: Stores a mutable `current` value.
- `RefCallback<T>`: Receives a mounted instance or `null` and can return a cleanup function.
- `Ref<T>`: Accepts a callback ref, an object ref, or `null`.

### Props and component types

- `Attributes`: Supplies `key` and the optional `jsx` marker.
- `ClassAttributes<T>`: Adds `ref` support to `Attributes`.
- `RenderableProps<P, RefType>`: Combines component props with `children` and `ref`.
- `ComponentType<P>`: Matches either a `ComponentClass<P>` or a `FunctionComponent<P>`.
- `ComponentProps<C>`: Resolves the props type for a component type or a JSX intrinsic element name.
- `FunctionComponent<P>`: Describes a function component that returns `ComponentChildren`.
- `ComponentClass<P, S>`: Describes a class component constructor and its static helpers.
- `ComponentConstructor<P, S>`: Alias for a component class constructor.
- `AnyComponent<P, S>`: Accepts either a function component or a class component constructor.

### Context and error types

- `Consumer<T>`: Describes the context consumer component.
- `Provider<T>`: Describes the context provider component.
- `Context<T>`: Describes the full context object with `Provider`, `Consumer`, and optional `displayName`.
- `ContextType<C>`: Extracts the value type from a context object.
- `ErrorInfo`: Provides the optional `componentStack` string passed to error handling.

## Examples

### Render and update a tree

```js
import { h, render } from 'preact';

const app = document.getElementById('app');

render(
  <main>
    <h1>Hello</h1>
    <p>First render</p>
  </main>,
  app
);

render(
  <main>
    <h1>Hello</h1>
    <p>Updated content</p>
  </main>,
  app
);
```

### Clone an existing element

```js
import { h, cloneElement } from 'preact';

const button = <button class="primary">Save</button>;

const disabledButton = cloneElement(button, {
  disabled: true,
  class: 'primary is-disabled'
});

export const view = <div>{disabledButton}</div>;
```