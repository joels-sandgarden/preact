# Packages

## Overview

`preact` splits core behavior into a small root package and focused add-ons.

## Core package

- `preact` exports rendering, hydration, components, context, clone helpers, and `options`.

## Add-ons and companion packages

| Package | Purpose | Notes |
| --- | --- | --- |
| `preact-compat` | React compatibility layer | Maps React-style APIs to `preact`.
| `preact-hooks` | Hooks API | Provides state, effect, memo, context, and error boundary helpers.
| `jsx-runtime` | Automatic JSX runtime | Supports `jsx`, `jsxs`, and `jsxDEV`.
| `preact-debug` | Development diagnostics | Adds prop warnings and component stack helpers.
| `preact-devtools` | Devtools bridge | Initializes devtools support and forwards hook names.
| `test-utils` | Test helpers | Exposes `act`, rerender setup, and teardown.

## Related pages

- [Overview](./overview.md)
- [Core architecture](./architecture.md)
- [Development workflow](./development.md)