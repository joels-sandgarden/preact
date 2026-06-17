# Repository layout

## Root package entry points

The root `package.json` defines the package name, entry fields, and export map.

- `main` points CommonJS consumers to `dist/preact.js`.
- `module` points ESM consumers to `dist/preact.mjs`.
- `umd:main` points UMD consumers to `dist/preact.umd.js`.
- `source` points build tools to `src/index.js`.
- The root export map exposes `preact`, `preact/compat`, `preact/debug`, `preact/devtools`, `preact/hooks`, `preact/test-utils`, `preact/compat/test-utils`, `preact/jsx-runtime`, `preact/jsx-dev-runtime`, `preact/compat/client`, `preact/compat/server`, `preact/compat/server.browser`, `preact/compat/jsx-runtime`, `preact/compat/jsx-dev-runtime`, and `preact/compat/scheduler`.
- Each package also exports its own `package.json` file.

## Repository layout

- `src/` holds the core implementation.
- `compat/` holds React compatibility code, package entry points, and compatibility tests.
- `debug/` holds debugging support code and browser tests.
- `devtools/` holds DevTools integration code and browser tests.
- `hooks/` holds hook APIs and browser tests.
- `jsx-runtime/` holds JSX runtime entry points and browser tests.
- `test-utils/` holds shared test helpers and tests.
- `demo/` holds example applications and demo assets.
- `test/` holds the main test suite, shared tests, node tests, and TypeScript tests.

## Package relationships

- `compat` builds the React-compatible surface on top of the core package.
- `hooks` provides hook APIs through a separate package entry point.
- `debug` adds debugging support and diagnostic helpers.
- `devtools` adds integration hooks for Preact DevTools.
- `jsx-runtime` provides the JSX runtime entry points used by modern JSX transforms.
- `test-utils` provides testing helpers that support the core package and compatibility tests.
- The root package maps both `preact/test-utils` and `preact/compat/test-utils` to the same helper package.

## Contributor navigation

1. Start implementation work in `src/`.
2. Check package-specific code in `compat/src/`, `hooks/src/`, `debug/src/`, `devtools/src/`, `jsx-runtime/src/`, and `test-utils/src/`.
3. Read matching tests in `test/` and each package's `test/` directory.
4. Use `demo/` for application-level examples.

## Scripts

### Build

- `build` runs all build jobs in parallel.
- `build:core` bundles the root package.
- `build:compat`, `build:debug`, `build:devtools`, `build:hooks`, `build:test-utils`, and `build:jsx` bundle the related packages.
- `dev`, `dev:hooks`, and `dev:compat` run watch builds for the root package and selected packages.

### Test

- `test` runs build, lint, and unit tests.
- `test:unit` runs `test:vitest:min` and `test:ts`.
- `test:vitest`, `test:vitest:min`, and `test:vitest:watch` cover the Vitest workflows.
- `test:ts`, `test:ts:core`, and `test:ts:compat` run type checks for the core and compat packages.

### Lint and formatting

- `lint` runs `oxlint` and `tsc`.
- `format` and `format:check` run Biome formatting.