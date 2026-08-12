# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

This release candidate rolls up bundle size, diffing, hydration, hooks, and compatibility improvements for Preact v11.

## Additional Changes

* Updated version metadata and the devtools attachment to `11.0.0-rc.0`.
* Reduced compressed and bundled output through updated name mangling and expression level reductions.
* Optimized keyed reorder diffing while preserving bounded longest increasing subsequence (LIS) behavior, lowering diff overhead for reordered children.
* Restored `_bits` name mangling for the Preact ISO target, correcting its internal property mapping.
* Deferred passive effect cleanup on unmount to align with v11 timing.
* Preserved `constructor` when cloning virtual nodes, preventing runtime errors in hardened JavaScript and frozen intrinsics environments.

## Bug Fixes

* Corrected hydration handling for excess markers and improved ref application during diffing.
* Strengthened compatibility validation by rejecting boxed React element symbols as invalid elements.

## Breaking Changes

* Confirmed that no breaking changes were identified for this release candidate.