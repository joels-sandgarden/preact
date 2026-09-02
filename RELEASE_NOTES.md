# v1.0.2-test

### Bug Fixes

* Reduced the compressed core size while preserving efficient bounded searches for keyed list reordering.
* Updated package and developer tool version information to `11.0.0-rc.0`.
* Streamlined keyed list updates so insertion and removal take less processing.
* Improved server rendered startup by handling extra markers correctly and applying references more consistently.
* Restored expected internal property mapping in Preact ISO builds.
* Trimmed generated output in compatibility packages and the JSX runtime.
* Corrected passive effect cleanup timing to match v11 behavior when components unmount.
* Improved cloning in restricted JavaScript environments by preserving constructor information.
* Clarified compatibility behavior for boxed React element symbols.