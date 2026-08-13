# Changelog

## v11.0.0-rc.0

- Reduced compressed and bundled artifact sizes by protecting private property aliases in `mangle.json` and simplifying code across core, compat, hooks, and `jsx-runtime`.
- Improved keyed reorder diffing with local hoisting in `constructNewChildrenArray` and adjusted longest increasing subsequence lookups, including bounded lookups.
- Improved hydration handling for excess markers and added guards around `commitRoot` and refs.
- Restored `_bits` mangling for Preact ISO builds.
- Deferred passive effect cleanup until unmount in the hooks implementation.
- Preserved VNode constructors when cloning VNodes for hardened and frozen intrinsics environments.
- Rejected boxed React element symbols during compat validation.