 # v11.0.0-rc.0

The v11.0.0-rc.0 release candidate delivers smaller build artifacts and more reliable rendering, hydration, effects, and compatibility behavior.

## Improvements and fixes

* Reduced the compressed core bundle size while preserving efficient lookup for keyed list updates.
* Trimmed additional bundle size from the release candidate's build artifacts.
* Improved keyed list reordering to reduce the work required during diffing.
* Corrected hydration handling for excess markers to improve server-rendered UI updates.
* Refined commit and ref processing to make UI updates more reliable.
* Deferred passive effect cleanup to the intended v11 timing.
* Strengthened vnode cloning compatibility in hardened JavaScript environments.
* Restored the `_bits` property mangle for the Preact ISO target so its internal property mapping remains correct.
* Updated package metadata and the devtools attachment to v11.0.0-rc.0.
* Enhanced compatibility validation for React elements that use boxed symbols.