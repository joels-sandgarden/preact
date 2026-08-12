# v11.0.0-rc.0: bundle size reductions and diffing improvements

2026-08-12

Version `11.0.0-rc.0`

This release candidate rolls the latest size and diffing work into the `11.0.0-rc.0` release. It keeps the public surface stable while tightening the runtime and reducing output size.

## Additional Changes

* Trimmed the core bundle size while preserving the lookup used when reordering keyed content.
* Refined diffing behavior to reduce extra work during updates.
* Reduced supporting bundle size across the runtime helpers.
* Restored `_bits` mangling for ISO builds to keep the release output compact.
* Cut `11.0.0-rc.0` as the release candidate.