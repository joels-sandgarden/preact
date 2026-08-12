# Preact v11.0.0-rc.0: Reduce bundle size and improve diffing

## Version

`11.0.0-rc.0`

## Summary

Preact v11.0.0-rc.0 reduces minified build sizes, lowers overhead in keyed reorder diffing, and improves runtime correctness and compatibility across core and related packages.

## Performance

* Reduced minified core artifacts to make builds smaller.
* Trimmed compatibility, hooks, and JSX runtime output to further reduce minified artifacts.
* Streamlined list reordering to lower diffing overhead.

## Correctness and Compatibility

* Improved diffing and hydration behavior by handling unexpected markers, applying refs consistently, and protecting runtime checks.
* Restored correct internal property mapping for Preact ISO builds.
* Deferred cleanup for passive effects during unmount to the intended v11 timing.
* Preserved constructor fields while cloning virtual nodes to reduce errors in hardened JavaScript environments.
* Strengthened compatibility validation by rejecting wrapped React element symbols.

## Additional Changes

* Updated release metadata across packages and developer tools to identify version `11.0.0-rc.0`.