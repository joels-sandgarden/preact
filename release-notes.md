# Preact v11.0.0-rc.0

**Release date:** 2026-08-12  
**Version:** `11.0.0-rc.0`

This prerelease reduces the core bundle size and improves rendering, hydration, effect cleanup, and compatibility behavior.

## Highlights

* Updated the release version and devtools attachment to `11.0.0-rc.0`.
* Reduced the compressed core bundle size through smaller runtime expressions and more effective private property mangling across compatibility, hooks, and JSX runtime modules.
* Improved keyed list reordering to make reconciliation more efficient.
* Restored the expected internal property mapping for the Preact ISO target.

## Fixes

* Improved hydration handling when the rendered output contains excess markers.
* Simplified ref application and added safer checks around guarded rendering paths.
* Deferred passive effect cleanup until after unmount processing completes.
* Preserved the `constructor` field when cloning virtual nodes in hardened JavaScript environments.
* Enhanced compatibility with boxed React element symbols.
