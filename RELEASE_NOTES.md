# v1.0.2-test

### Enhancements

* Reduced core compressed size while preserving bounded list lookup.
* Shortened expressions to streamline generated output.
* Improved keyed content reordering for more consistent updates.
* Restored compact naming in ISO builds.

### Bug Fixes

* Corrected the application of server-rendered content and reference handling during root updates.
* Deferred passive effect cleanup until unmount completed.
* Preserved constructors when cloning elements in hardened environments.
* Improved compatibility with boxed React element symbols.