# Changelog

## v11.0.0-rc.0

- Reduced compressed and bundled artifact sizes through protected and private property aliases in `mangle.json`, along with code simplifications across core, compat, hooks, and `jsx-runtime`.
- Improved keyed reorder diffing by hoisting `_children` locally in `constructNewChildrenArray` and refining longest increasing subsequence and bounded lookup adjustments.
- Improved excess marker handling during hydration and added guards around `commitRoot` and refs.
- Restored `_bits` mangling for Preact ISO builds.
- Deferred passive effect cleanup until unmount in hooks.
- Preserved VNode constructors when cloning VNodes in environments with hardened or frozen intrinsics.
- Rejected React element symbols boxed in objects during compat validation.
- No breaking changes were reported for this release candidate.