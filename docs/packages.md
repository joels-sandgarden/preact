# Packages

## Overview

`preact` splits core behavior into a small root package and focused add-ons.

## Core package

- `preact` exports rendering, hydration, components, context, clone helpers, and `options`.
- The root package publishes source from `src/` and compiled output from `dist/`.

## `compat`

- `compat` exports the React-compatible surface that mirrors the APIs most applications expect from React.
- It builds on the core runtime so existing React-oriented code can render through `preact` without rewriting every component.
- It exists to make migration practical when a codebase depends on React conventions and wants a smaller runtime.

## `hooks`

- `hooks` exports state, effect, memo, callback, ref, context, and reducer helpers for function components.
- It layers on top of the core component model and shares the same update cycle as the rest of `preact`.
- It exists to give function components the same stateful building blocks that class components and framework-style integrations already rely on.

## `debug`

- `debug` exports development-only warnings and helpers that explain invalid props, usage mistakes, and component state during development.
- It reads the same component data that the core runtime tracks, then reports that information in a clearer form.
- It exists to make integration issues easier to spot before they reach production.

## `devtools`

- `devtools` exports the bridge that lets browser devtools inspect the component tree and hook activity.
- It connects to the core runtime through the shared options hook and forwards runtime events to the inspection tools.
- It exists to make interactive debugging and performance inspection work with `preact` applications.

## `jsx-runtime`

- `jsx-runtime` exports `jsx`, `jsxs`, and `jsxDEV` for the automatic JSX transform.
- It feeds JSX output into the core vnode creation path, so compiled JSX lands in the same render pipeline as handwritten vnode code.
- It exists to support modern JSX compilation without requiring a separate `h` import in every file.

## `test-utils`

- `test-utils` exports `act`, rerender helpers, and cleanup helpers for tests.
- It drives the core runtime through controlled updates so assertions see settled component state.
- It exists to make component tests predictable when updates happen asynchronously.

## Related pages

- [Overview](./overview.md)
- [Core architecture](./architecture.md)
- [Development workflow](./development.md)