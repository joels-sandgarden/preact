# `preact/compat`

## Overview

`preact/compat` provides a React compatible facade over Preact for third party packages that expect React APIs. It keeps Preact as the renderer and exposes the runtime surface that common ecosystem tools look for.

## Runtime components

- `Component` and `PureComponent` let class components follow the React component model.
- `Fragment` groups children without adding an extra DOM element.
- `StrictMode` points to `Fragment` in the compatibility layer.
- `Suspense` and `lazy` support deferred component loading.
- `memo` and `forwardRef` expose the standard React memoization and ref forwarding helpers.

## Rendering helpers

- `render(vnode, parent, callback?)` mounts a tree into a DOM container.
- `hydrate(vnode, parent, callback?)` attaches to existing server rendered markup.
- `unmountComponentAtNode(container)` clears a mounted tree from a container and returns `true` when it removes content.
- `createPortal(vnode, container)` renders children into a separate DOM node while keeping them in the same component tree.

## Element utilities

- `Children` provides `map`, `forEach`, `count`, `only`, and `toArray` for child collection handling.
- `createElement(type, props, ...children)` builds virtual elements.
- `createContext(defaultValue)` creates a context object for shared state.
- `createFactory(type)` returns a helper that always creates the same element type.
- `cloneElement(element, props?, ...children)` copies an element and applies new props or children.
- `createRef()` creates an object ref with a mutable `current` value.
- `findDOMNode(component)` resolves the DOM node for a mounted component or returns `null` when no node exists.
- `isValidElement(value)` checks whether a value matches the React element shape.
- `isFragment(value)` checks whether a value represents a fragment.
- `isMemo(value)` checks whether a value represents a memoized component.

## Hooks and concurrent helpers

`preact/compat` re-exports these hooks from `preact/hooks`:

- `useCallback`
- `useContext`
- `useDebugValue`
- `useEffect`
- `useId`
- `useImperativeHandle`
- `useLayoutEffect`
- `useMemo`
- `useReducer`
- `useRef`
- `useState`

The compatibility layer also exposes React 18 style helpers:

- `useInsertionEffect` runs after a render but before layout work.
- `startTransition(callback)` marks an update as non urgent.
- `useDeferredValue(value)` returns a deferred version of a value.
- `useSyncExternalStore(subscribe, getSnapshot)` reads an external store safely.
- `useTransition()` returns transition state and a start function.
- `flushSync(callback, arg?)` runs a callback and forces synchronous rendering around it.
- `unstable_batchedUpdates(callback, arg?)` executes a callback without adding extra batching overhead.

## Compatibility only exports

- `version` exposes the React version string that many packages read during feature checks.
- The default export object mirrors the named exports so React style imports continue to work.
- `isElement` aliases `isValidElement` for packages that expect the older helper name.

## Alias entry points

- `preact/compat/jsx-runtime` passes through to the top level JSX runtime after loading `preact/compat`.
- `preact/compat/jsx-dev-runtime` passes through to the top level JSX runtime after loading `preact/compat`.
- `preact/compat/test-utils` passes through to the top level test utils module.
- `preact/compat/server.browser` exposes the browser targeted server rendering variant with `renderToString` and `renderToStaticMarkup`.

## React style interoperability example

```jsx
import React, { useState } from 'preact/compat';

function Counter() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

export default Counter;
```
