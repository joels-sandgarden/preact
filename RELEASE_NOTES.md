# v1.0.2-test

### Enhancements

* Reduced core compressed size without changing list lookup limits.
* Streamlined generated output with shorter expressions and compact naming.
* Improved keyed content reordering while retaining its bounded lookup path.
* Restored compact naming for the ISO build.

### Bug Fixes

* Corrected server rendered content hydration and reference handling during root updates.
* Deferred passive effect cleanup until unmount completes.
* Preserved constructors when cloning elements in hardened environments.
* Improved compatibility with boxed React element symbols.