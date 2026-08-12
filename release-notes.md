# Preact v11.0.0-rc.0

## Release candidate

**Version:** `11.0.0-rc.0`

This release candidate delivers smaller distributed files, more efficient rendering updates, and broader compatibility across Preact and its related packages.

## Highlights

* Updated package metadata and the developer tools attachment to identify version `11.0.0-rc.0`.
* Reduced minified bundle and core compressed sizes with smaller expressions and more effective property naming.
* Improved keyed component reordering to reduce rendering overhead while preserving optimized searches for bounded reorder cases.
* Refined server rendered content marker handling, simplified reference application after rendering, and made safety checks more consistent.

## Fixes and improvements
* Restored reliable internal naming in Preact ISO builds so minified runtime access works as intended.
* Adjusted unmount timing so passive effects clean up according to intended v11 behavior.
* Preserved constructor metadata when copying virtual nodes, improving behavior in hardened JavaScript and frozen intrinsics environments.
* Tightened compatibility element validation to reject React elements that use boxed symbols.

## Upgrade context

This release candidate introduces no breaking changes. Smaller outputs, rendering updates, server rendered content handling, and compatibility fixes apply when adopting version `11.0.0-rc.0`.