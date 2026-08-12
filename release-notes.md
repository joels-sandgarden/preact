# Preact v11.0.0-rc.0

## Release candidate

**Version:** `11.0.0-rc.0`

This release candidate focuses on smaller distributed files, more efficient rendering updates, and compatibility improvements across Preact and its related packages.

## Highlights

* Updated package metadata and the developer tools attachment to identify version `11.0.0-rc.0`.
* Reduced minified bundle and core compressed sizes through smaller expressions and more effective private property naming.
* Improved keyed component reordering to reduce overhead while preserving the bounded longest increasing subsequence optimization.
* Refined hydration handling for excess markers, simplified reference application after rendering, and made guarded checks more consistent.

## Fixes and improvements
* Restored reliable property mapping in Preact ISO builds so minified runtime access works as intended.
* Deferred passive effect cleanup during unmount to match the intended v11 timing.
* Preserved constructor metadata when cloning VNodes, improving behavior in hardened JavaScript and frozen intrinsics environments.
* Tightened compatibility element validation to reject boxed React element symbols.

## Upgrade context

No breaking changes are included in this release candidate. The smaller outputs, rendering updates, hydration handling, and compatibility fixes apply when adopting version `11.0.0-rc.0`.