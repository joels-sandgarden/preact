# v11.0.0-rc.0

2026-08-12

Version `11.0.0-rc.0`

This release candidate rolls up the latest bundle size and diffing work ahead of the `11.0.0-rc.0` cut. It keeps the public surface stable while making the runtime smaller and the update path more efficient.

## Additional Changes

* Improved the core bundle size while preserving the lookup used when reordering keyed content.
* Refined update handling to reduce extra work during content changes.
* Reduced supporting bundle size across the runtime.
* Restored `_bits` mangling for ISO builds so release output stays compact.
* Released `11.0.0-rc.0` as the new release candidate.