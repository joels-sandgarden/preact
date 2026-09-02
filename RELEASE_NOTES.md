# v1.0.2-test

### Enhancements

* Reduced core compressed size while preserving bounded lookup behavior.
* Optimized generated bundles through safer name mangling and shorter expressions.
* Improved keyed list reordering so updates retain efficient bounded lookup behavior.
* Restored compact internal naming in the ISO build.

### Bug Fixes

* Corrected hydration and root update handling for references.
* Deferred passive effect cleanup until components unmount.
* Preserved element constructors when cloning virtual elements in hardened environments.
* Validated compatibility with boxed React element symbols.