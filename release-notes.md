# 11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Summary

Version `11.0.0-rc.0` makes the v11 release candidate available with smaller compressed outputs, more efficient keyed updates, stronger hydration and runtime correctness, improved compatibility in hardened JavaScript environments, and corrected property mapping for the Preact ISO target.

## Changes

* Updated package metadata and developer tooling to `11.0.0-rc.0`, making the v11 release candidate available.

* Reduced compressed core output size through property mangling and restored the `_bits` property mapping for the Preact ISO target.

* Optimized keyed list updates and the bounded longest increasing subsequence path by reusing the new children array and simplifying insertion and unmount handling.

* Improved streamed hydration excess marker handling, portal and ref commits, virtual node cloning, and frequently used diff paths for more reliable runtime behavior.

* Refined state cloning and DOM sibling and insertion bookkeeping to improve component updates.

* Adjusted pending effect argument commits and related frequently used paths for more consistent hook behavior.

* Hardened compatibility by rejecting boxed React element symbols and strengthening virtual node cloning behavior.

* Minimized expressions in the JSX runtime and compatibility layers to reduce generated output size.

* Removed the internal `_contextRef` tracking and simplified subscriber cleanup for context updates.

* Simplified style clearing and listener initialization to reduce update overhead.

* Eliminated obsolete `_contextRef` declarations from internal type definitions to keep the context model consistent.