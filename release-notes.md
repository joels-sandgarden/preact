# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

This release candidate rolls up bundle size, diffing, hydration, hooks, and compatibility improvements for Preact v11.

## Additional Changes

* Updated version metadata and the devtools attachment to `11.0.0-rc.0`.
* Reduced compressed and bundled output through updated name mangling and expression level reductions.
* Optimized keyed reorder diffing while preserving bounded longest increasing subsequence (LIS) behavior, lowering diff overhead for reordered children.

## Bug Fixes

* Corrected hydration handling for excess markers and improved ref application during diffing.

## Breaking Changes

* Confirmed that no breaking changes were identified for this release candidate.