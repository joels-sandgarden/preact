# v11.0.0-rc.0: Bundle size and diffing improvements

**Date:** 2026-08-12

**Version:** 11.0.0-rc.0

## Summary

This release reduces generated output sizes and improves how Preact updates keyed lists, hydrated content, references, and lifecycle effects. It also strengthens compatibility behavior in hardened environments and adds stricter React element validation.

## Performance

* Reduced compressed and bundled output sizes across the core, compat, hooks, and JSX runtime packages by aliasing repeated properties and simplifying generated expressions.

* Restored `_bits` name compression for Preact ISO builds, reducing their generated output size.

## Enhancements

* Improved keyed list reordering with more efficient sequence matching, reducing unnecessary work when items change position.

* Refined hydration and root updates so references receive consistent handling while rendered content is committed.

## Bug Fixes

* Deferred passive effect cleanup until after unmount processing completes, preserving expected cleanup timing for hooks.

* Preserved virtual node constructors when cloning nodes in hardened environments, including environments with frozen built-ins.

## Additional Changes

* Strengthened compatibility validation so boxed React element symbols no longer pass as valid React elements.

* Recognized joel-solymosi as the first contributor to Preact.
