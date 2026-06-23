# Development Workflow

## Overview

`preact` uses npm scripts for builds, linting, formatting, and test runs.

## Setup

1. Install dependencies with `npm install`.
2. Run `npm run test:install` if Chromium is not available for browser tests.

## Common tasks

- `npm run dev` watches the core package.
- `npm run dev:hooks` and `npm run dev:compat` watch the add-ons.
- `npm test` runs build, lint, and unit tests.
- `npm run build` produces package artifacts across the repository.
- Run `npm run build` after source changes to refresh generated package output.
- `npm run lint` runs `oxlint` and `tsc`.
- `npm run format` and `npm run format:check` keep formatting consistent.
- `npm run test:vitest`, `npm run test:ts`, and `npm run test:vitest:watch` target specific suites.

## Working habits

- Keep changes aligned with `src/`, package subdirectories, and their tests.
- Check generated `dist/` output only after a build.

## Related pages

- [Overview](./overview.md)
- [Core architecture](./architecture.md)
- [Packages](./packages.md)