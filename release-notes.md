# v11.0.0-rc.0: Bundle Size and Diffing Improvements

**Version:** `11.0.0-rc.0`

This release candidate delivers smaller compressed bundles, more efficient updates for reordered content, more reliable hydration, and improved compatibility across supported environments.

## Highlights

* Reduced the compressed core bundle size by shortening protected and private property names and simplifying expressions across the compatibility, hooks, and JSX runtime packages.
* Improved keyed content reordering by refining the lookup process used to place existing content efficiently.
* Improved hydration handling for excess markers so the client can reconcile server rendered content more reliably.
* Refined guarded rendering checks and ref application for more consistent updates.
* Restored `_bits` name compression for Preact ISO builds while preserving the runtime access those builds expect.
* Deferred passive effect cleanup during unmount to preserve expected cleanup timing.

## Fixes

* Fixed vnode cloning in hardened JavaScript and frozen intrinsics environments by retaining the constructor field.
* Corrected compatibility validation so boxed React element symbols are rejected.

## Release Metadata

* Updated package metadata and the DevTools attachment to identify version `11.0.0-rc.0`.

## Compatibility

No breaking changes were identified for this release candidate.