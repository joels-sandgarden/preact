# Development Workflow

## Overview

This guide covers local setup, the main development scripts, branch and release practices, and the repository areas that maintainers review most often.

## Setup

1. Install dependencies with `npm install`.
2. Run `npm run test:install` when Chromium is unavailable and browser tests need a local installation.

## Branch and release conventions

- Use short, topic-based branch names that describe the change.
- Keep each branch focused on a single piece of work so reviews stay small and clear.
- Prepare release work only after the full build, lint, and test flow passes on the repository.
- Treat released versions as the result of the normal build and test process.

## Common tasks

- `npm run dev` watches the core package during local development.
- `npm run dev:hooks` watches the hooks add-on.
- `npm run dev:compat` watches the compat add-on.
- `npm test` runs the build, lint, and unit test steps together.
- `npm run build` creates package artifacts across the repository and refreshes generated package output.
- `npm run lint` runs `oxlint` and `tsc` to catch code quality and type issues.
- `npm run format` applies the repository format rules.
- `npm run format:check` verifies formatting without changing files.
- `npm run test:vitest` runs the Vitest suite.
- `npm run test:ts` runs the TypeScript-focused checks.
- `npm run test:vitest:watch` keeps the Vitest suite running in watch mode.

## Repository structure

- Keep source changes in `src/` and in the package directories that own the behavior.
- Add or update tests beside the code they cover.
- Review `dist/` and similar generated output only after a build refreshes it.
- Treat generated files as build results and leave them untouched unless a build changes them.

## Related pages

- [Overview](./overview.md)
- [Core architecture](./architecture.md)
- [Packages](./packages.md)