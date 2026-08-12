# v11.0.0-rc.0: Bundle Size and Diffing Improvements

**Version:** `11.0.0-rc.0`

This release candidate delivers smaller compressed bundles, more efficient updates for reordered content, more reliable hydration, and improved compatibility across supported environments.

## Highlights

* Reduced the compressed core bundle size by shortening internal property names and simplifying expressions across the compatibility, hooks, and JSX runtime packages.
* Enhanced list updates after items change order by refining how existing items find their new positions.
* Strengthened server rendered content reconciliation by handling extra markers more reliably.
* Refined conditional rendering checks and reference updates for more consistent results.
* Restored `_bits` compression for Preact ISO builds while preserving the runtime access those builds expect.
* Deferred passive effect cleanup during unmount to preserve expected cleanup timing.

## Fixes

* Fixed element cloning in hardened JavaScript environments and environments with frozen built in objects by retaining constructor information.
* Corrected compatibility validation so it rejects boxed React element symbols.

## Release Metadata

* Updated package metadata and the DevTools attachment to identify version `11.0.0-rc.0`.

## Compatibility

This release candidate introduces no identified breaking changes.