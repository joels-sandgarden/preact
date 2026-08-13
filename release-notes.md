# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Version

`v11.0.0-rc.0`

## Summary

This release candidate reduces production bundle size and improves update handling for reordered content, hydration, lifecycle cleanup, and compatibility with hardened JavaScript environments.

## Additional Changes

* Added the `v11.0.0-rc.0` release candidate with synchronized package and DevTools version identifiers.

## Performance

* Reduced compressed and bundled core size through smaller production output across the compatibility, hooks, and JSX runtime packages.

## Rendering

* Improved keyed list reordering so updates preserve efficient item matching when order changes.
* Refined hydration to handle excess markers consistently.
* Simplified reference application during committed updates and strengthened guarded checks.

## Compatibility

* Restored the expected internal field mapping for Preact ISO builds to preserve target compatibility.
* Deferred passive effect cleanup during unmount until the appropriate lifecycle phase.
* Fixed virtual node cloning in environments that freeze built-in JavaScript objects by retaining constructor information.
* Strengthened compatibility validation by rejecting boxed React element symbols.