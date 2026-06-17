# Preact codebase guide

## Overview

Preact is a small React-compatible virtual DOM library. This guide points contributors to the main repository areas.

## Start here

- Read [`repo-layout.md`](./repo-layout.md) for the repository layout and package entry points.
- Review [`../README.md`](../README.md) for the project overview and getting started notes.
- Check [`../package.json`](../package.json) for the package export map and build scripts.

## Major areas

- `src/` contains the core implementation.
- `compat/` provides React compatibility entry points and related support files.
- `hooks/` contains hook APIs.
- `debug/` contains debugging support.
- `devtools/` contains DevTools integration.
- `jsx-runtime/` contains JSX runtime entry points.
- `test-utils/` contains shared test helpers.
- `test/` contains the main test suite.
- `demo/` contains example applications and demos.

## Contributor path

1. Start with `src/index.js` and the files it imports.
2. Use `package.json` to review the consumer entry points.
3. Read the relevant tests under `test/`, `compat/test/`, `hooks/test/`, `debug/test/`, `devtools/test/`, `jsx-runtime/test/`, and `test-utils/test/`.
4. Use `demo/` to see small examples and feature-specific usage.