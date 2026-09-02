# v1.0.2-test

### Bug Fixes

* Reduced core compressed size and preserved bounded lookup during keyed reorders.
* Updated package metadata and the developer tools attachment to `11.0.0-rc.0`.
* Improved keyed reorder processing to reduce overhead while maintaining correct insertion and removal behavior.
* Corrected hydration handling for excess markers and ref application to improve rendering consistency.
* Restored the correct internal property mapping for Preact ISO builds.
* Trimmed generated output in compatibility packages and the JSX runtime.
* Aligned passive effect cleanup timing with v11 behavior during unmount.
* Hardened vnode cloning for JavaScript environments with frozen built-ins by retaining constructor information.
* Strengthened compatibility validation for boxed React element symbols.