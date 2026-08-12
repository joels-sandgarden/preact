# Preact v11.0.0-rc.0: Reduce bundle size and improve diffing

## Version

`11.0.0-rc.0`

## Summary

Preact v11.0.0-rc.0 reduces minified build sizes, lowers overhead in keyed reorder diffing, and improves runtime correctness and compatibility across core and related packages.

## Performance

* Reduced compressed core size for smaller minified build artifacts.
* Trimmed expressions across the compatibility, hooks, and JSX runtime packages to further reduce minified output.
* Streamlined keyed reorder processing to lower diffing overhead.

## Correctness and Compatibility

* Improved diffing and hydration behavior by handling excess markers, applying refs more simply, and guarding checks consistently.
* Restored the correct `_bits` mapping for Preact ISO builds.
* Deferred passive effect cleanup on unmount to the intended v11 timing.
* Preserved constructor fields during VNode cloning to reduce errors in hardened JavaScript environments.
* Strengthened compatibility validation by rejecting boxed React element symbols.