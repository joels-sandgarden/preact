# v1.0.2-test

### Bug Fixes

* Reduced the compressed core size while preserving the bounded search used during keyed list reordering.
* Updated package and developer tooling version information to `11.0.0-rc.0`.
* Simplified keyed list updates so insertion and removal require less processing.
* Improved server rendered page startup when extra markers appear and made reference updates more consistent.
* Corrected internal property mapping in Preact ISO builds.
* Trimmed generated output in compatibility packages and the JSX runtime.
* Aligned passive effect cleanup timing with v11 behavior when components unmount.
* Hardened cloning in restricted JavaScript environments by preserving constructor information.
* Clarified compatibility handling for boxed React element symbols.