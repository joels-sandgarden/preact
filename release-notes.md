# 11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Summary

Version `11.0.0-rc.0` makes the v11 release candidate available with smaller compressed outputs, more efficient keyed updates, more reliable streamed hydration and runtime behavior, stronger compatibility in hardened JavaScript environments, and corrected property mapping for the Preact ISO target.

## Changes

* Updated package metadata and developer tooling to `11.0.0-rc.0`, making the v11 release candidate available.

* Reduced compressed core output size by shortening internal property names and restored the `_bits` mapping for the Preact ISO target.

* Optimized keyed list updates by reusing the new child list, improving the bounded ordering path, and simplifying insertion and removal handling.

* Improved streamed hydration when extra markers appear, along with portal updates, reference commits, virtual node copying, and frequently used update paths.

* Refined state cloning and DOM sibling and insertion bookkeeping to improve component updates.

* Adjusted pending effect argument commits and related frequently used paths for more consistent hook behavior.

* Hardened compatibility by rejecting boxed React element symbols and strengthening virtual node cloning behavior.

* Minimized expressions in the JSX runtime and compatibility layers to reduce generated output size.

* Removed the internal `_contextRef` tracking and simplified subscriber cleanup for context updates.

* Simplified style clearing and listener initialization to reduce update overhead.

* Eliminated obsolete `_contextRef` declarations from internal type definitions to keep the context model consistent.