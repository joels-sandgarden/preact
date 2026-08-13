# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Version

`v11.0.0-rc.0`

## Summary

This release candidate reduces production bundle size and improves how the library updates reordered content, server-rendered content, component removal, and compatibility with hardened JavaScript environments.

## Additional Changes

* Added the `v11.0.0-rc.0` release candidate with synchronized package and DevTools version identifiers.

## Performance

* Reduced compressed and bundled core size through smaller production output across the compatibility, hooks, and JSX runtime packages.

## Rendering

* Improved reordered list updates so the library preserves efficient item matching when order changes.
* Refined server-rendered content handling to ignore extra markers consistently.
* Simplified reference application during updates and strengthened safety checks.

## Compatibility

* Restored the expected field mapping for Preact ISO builds to preserve target compatibility.
* Deferred cleanup for effects that run outside rendering during component removal until the appropriate lifecycle phase.
* Fixed component node cloning in environments that freeze built-in JavaScript objects by retaining constructor information.
* Strengthened compatibility validation by rejecting wrapped React element symbols.