# v1.0.2-test

### Enhancements

* Reduced core compressed size while preserving predictable list matching.
* Made generated output smaller by shortening its expressions.
* Improved content reordering when item keys change for more consistent updates.
* Restored compact naming in ISO builds.

### Bug Fixes

* Corrected how server-rendered content and references apply during root updates.
* Deferred cleanup for effects that run after rendering until unmount completed.
* Preserved element constructors when cloning elements in hardened environments.
* Improved compatibility with wrapped React element symbols.