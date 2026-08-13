# Preact v11.0.0-rc.0

**Release date:** 2026-08-12  
**Version:** `11.0.0-rc.0`

This prerelease reduces the core bundle size and improves rendering, hydration, effect cleanup, and compatibility behavior.

## Highlights

* Updated the release version and devtools attachment to `11.0.0-rc.0`.
* Reduced the compressed core bundle size through smaller runtime expressions and tighter internal property encoding across compatibility, hooks, and JSX runtime modules.
* Improved keyed list reordering for more efficient updates.
* Restored the expected internal property mapping for the Preact ISO target.

## Fixes

* Improved hydration behavior when rendered output contains extra markers.
* Simplified ref handling and strengthened checks around rendering paths.
* Deferred effect cleanup until after unmount processing completes.
* Preserved the `constructor` field when cloning virtual nodes in hardened JavaScript environments.
* Enhanced compatibility with boxed React element symbols.
