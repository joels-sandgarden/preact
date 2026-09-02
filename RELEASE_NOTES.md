# v1.0.2-test

### Enhancements

* Reduced core compressed size while preserving bounded list lookup.
* Shortened expressions to streamline generated output.
* Improved keyed content reordering while retaining bounded lookup.
* Restored compact naming in ISO builds.

### Bug Fixes

* Corrected server-rendered content hydration and reference handling during root updates.
* Deferred passive effect cleanup until unmount completed.
* Preserved constructors when cloning elements in hardened environments.
* Improved compatibility with boxed React element symbols.