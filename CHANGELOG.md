# v1.0.2-test

### Bug Fixes

* Reduce the compressed core size and preserve bounded lookup behavior for keyed reorders.
* Improve hydration and diffing correctness, including handling for excess hydration markers and reference application.
* Reduce overhead during keyed reorders by simplifying insertion and unmount processing.
* Correct internal property mapping for Preact ISO builds.
* Defer passive effect cleanup during unmount to provide the intended v11 timing.
* Preserve vnode constructors during cloning for hardened JavaScript environments.
* Reject boxed React element symbols for more reliable compatibility behavior.
* Update package metadata and the devtools attachment to `11.0.0-rc.0`.

This release introduces no breaking changes.