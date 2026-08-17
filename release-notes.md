# v11.0.0-rc.0

The v11.0.0-rc.0 release candidate delivers smaller build artifacts and more reliable rendering, hydration, effects, and compatibility behavior.

## Improvements and fixes

* Reduced the compressed core bundle size while preserving efficient lookup for keyed list updates.
* Trimmed additional bundle size from the release candidate's build artifacts.
* Improved keyed list reordering to reduce the work required during diffing.
* Corrected hydration when extra server-rendered markers appear to improve UI updates.
* Refined reference updates during rendering to make UI changes more reliable.
* Deferred passive effect cleanup to the intended v11 timing.
* Strengthened component cloning compatibility in hardened JavaScript environments.
* Restored the `_bits` property mapping in Preact ISO builds to keep internal names aligned.
* Updated package metadata and the devtools attachment to v11.0.0-rc.0.
* Enhanced compatibility validation for React elements that use boxed symbols.