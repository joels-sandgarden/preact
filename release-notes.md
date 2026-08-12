# 11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Summary

Version `11.0.0-rc.0` makes the v11 release candidate available with smaller compressed outputs, more efficient keyed updates, stronger hydration and runtime correctness, improved compatibility in hardened JavaScript environments, and corrected property mapping for the Preact ISO target.

## Changes

* Updated package metadata and developer tooling to `11.0.0-rc.0`, making the v11 release candidate available.

* Reduced compressed core output size through property mangling and restored the `_bits` property mapping for the Preact ISO target.

* Optimized keyed list updates and the bounded longest increasing subsequence path by reusing the new children array and simplifying insertion and unmount handling.

* Improved streamed hydration excess marker handling, portal and ref commits, virtual node cloning, and frequently used diff paths for more reliable runtime behavior.