# Preact v11.0.0-rc.0: Reduce bundle size and improve diffing

## Version

`11.0.0-rc.0`

## Summary

Preact v11.0.0-rc.0 reduces minified build sizes, lowers overhead in keyed reorder diffing, and improves runtime correctness and compatibility across core and related packages.

## Performance

* Reduced compressed core size for smaller minified build artifacts.
* Trimmed expressions across the compatibility, hooks, and JSX runtime packages to further reduce minified output.
* Streamlined keyed reorder processing to lower diffing overhead.