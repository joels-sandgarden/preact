# 11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Summary

Version `11.0.0-rc.0` makes the v11 release candidate available with smaller compressed outputs, more efficient keyed updates, more reliable streamed hydration and runtime behavior, stronger compatibility in hardened JavaScript environments, and corrected property mapping for the Preact ISO target.

## Changes

* Updated package metadata and developer tooling to `11.0.0-rc.0`, making the v11 release candidate available.

* Reduced compressed core output size by shortening internal property names and restored the `_bits` mapping for the Preact ISO target.

* Optimized keyed list updates by reusing the new child list, improving the bounded ordering path, and simplifying insertion and removal handling.

* Improved streamed hydration when extra markers appear, along with portal updates, reference commits, virtual node copying, and frequently used update paths.

* Refined component state copying and tracking for neighboring elements and insertions to improve component updates.

* Adjusted how pending hook effects apply their arguments and optimized related frequently used paths for more consistent hook behavior.

* Hardened compatibility in strict JavaScript environments by rejecting boxed React element symbols and making virtual node copying more reliable.

* Minimized expressions in the JSX runtime and compatibility layers, reducing generated output size.

* Removed the internal `_contextRef` reference and simplified subscriber cleanup for context updates.

* Simplified style reset and event listener setup to reduce update overhead.

* Eliminated obsolete `_contextRef` declarations from internal type definitions so declared context behavior matches runtime behavior.