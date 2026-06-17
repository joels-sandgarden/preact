# `preact/hooks`

## Overview

This document describes the hook API exported by `preact/hooks` and the way it coordinates state, effects, refs, context, diagnostics, error handling, and stable IDs during rendering.

## Prerequisites

- Basic familiarity with Preact components and JSX.
- An import from `preact/hooks` for the hook functions listed in this guide.

## Exported helper types

- `Dispatch<A>`: A function that accepts one value of type `A` and returns nothing.
- `StateUpdater<S>`: A value of type `S` or a function that accepts the previous state and returns the next state.
- `Reducer<S, A>`: A function that accepts the previous state and an action, then returns the next state.

## State hooks

### `useState`

`useState` returns a state value and an update function.

- Pass an initial value or a function that returns the initial value.
- Call the update function with a new value or with a function that receives the previous value.
- Use the updater form when the next state depends on the current state.

```js
import { useState } from 'preact/hooks';

const [count, setCount] = useState(0);
setCount(value => value + 1);
```

### `useReducer`

`useReducer` returns a state value and a `dispatch` function.

- Pass a reducer that accepts the current state and an action.
- Pass an initial state, or pass an initial value together with an initializer function.
- Use this hook when a component manages related state transitions in one place.

```js
import { useReducer } from 'preact/hooks';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return state + 1;
    default:
      return state;
  }
}

const [count, dispatch] = useReducer(reducer, 0);
dispatch({ type: 'increment' });
```

## Ref and context hooks

### `useRef`

`useRef` returns a mutable object with a `current` property.

- The object stays the same for the full lifetime of the component.
- Store mutable values there when a change should not trigger a rerender.
- Use it for DOM references and for instance-like values that must survive rerenders.

```js
import { useRef } from 'preact/hooks';

const inputRef = useRef(null);
```

### `useContext`

`useContext` returns the value from the nearest matching provider.

- The hook falls back to the context default value when no provider exists.
- The component rerenders when the provider updates.

```js
import { createContext } from 'preact';
import { useContext } from 'preact/hooks';

const ThemeContext = createContext('light');
const theme = useContext(ThemeContext);
```

### `useImperativeHandle`

`useImperativeHandle` customizes the value attached to a ref.

- Pass the target ref and a factory that returns the exposed object.
- Provide dependency values when the exposed handle should refresh only for specific changes.
- Pair it with `useRef` or a callback ref when a component needs to expose a small imperative surface.

## Effect hooks

### `useEffect`

`useEffect` runs after the browser paints.

- Use it for work that can wait until the screen updates.
- Return a cleanup function when the effect needs to release resources or cancel work.
- The hook compares each dependency array entry by identity with `Object.is`.

```js
import { useEffect } from 'preact/hooks';

useEffect(() => {
  const timer = setInterval(() => {
    console.log('tick');
  }, 1000);

  return () => clearInterval(timer);
}, []);
```

### `useLayoutEffect`

`useLayoutEffect` runs synchronously after DOM mutation and before the browser paints.

- Use it when code must read layout or adjust the DOM before the user sees the frame.
- The hook compares each dependency array entry by identity with `Object.is`.
- `useImperativeHandle` uses layout timing so ref updates land before paint.

## Memoization and callback helpers

### `useCallback`

`useCallback` returns the same function reference until one of the dependencies changes by identity.

- Use it to preserve function identity across rerenders.
- Pass the full dependency list so the callback always sees the values it reads.

### `useMemo`

`useMemo` returns a cached value from a factory function.

- The hook recomputes the value only when one of the dependencies changes by identity.
- Use it for expensive calculations or for values that need a stable reference.

## Diagnostics

### `useDebugValue`

`useDebugValue` sends a label or formatted value to developer tools.

- Pass a value directly when the label already reads well.
- Pass a formatter when the displayed value needs a custom shape.

## Error handling

### `useErrorBoundary`

`useErrorBoundary` returns `[error, reset]`.

- `error` holds the most recent error caught by the component.
- `reset` clears the stored error so rendering can continue.
- Pass a callback when the component should react to the error and inspect the accompanying `ErrorInfo` value.

### `useId`

`useId` returns a stable string for the lifetime of the component.

- The generated value stays stable within a root.
- The generated value also stays stable within the nearest async boundary.
- Use it for accessible relationships such as `aria-labelledby` and `htmlFor`.

## Example

The following example combines state, an effect, and context:

```js
import { createContext } from 'preact';
import { useContext, useEffect, useState } from 'preact/hooks';

const ThemeContext = createContext('light');

function CounterPanel() {
  const theme = useContext(ThemeContext);
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `${theme} count: ${count}`;
    return () => {
      document.title = 'preact';
    };
  }, [theme, count]);

  return (
    <button onClick={() => setCount(value => value + 1)}>
      {theme}: {count}
    </button>
  );
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <CounterPanel />
    </ThemeContext.Provider>
  );
}
```

The same pattern works with `useErrorBoundary` when a component needs to recover from a rendering error and reset its own error state.