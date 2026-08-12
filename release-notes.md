# Preact v11.0.0-rc.0

## Release candidate

**Version:** `11.0.0-rc.0`

This release candidate provides smaller distributed files, faster rendering updates, and more reliable behavior across Preact and its related packages.

## Highlights

* Updated package metadata and developer tools to identify version `11.0.0-rc.0`.
* Reduced minified bundle and core compressed sizes through leaner expressions and more effective property naming.
* Improved keyed component reordering with faster bounded searches and lower rendering overhead.
* Refined server rendered content markers, simplified reference application after rendering, and strengthened safety checks.

## Fixes and improvements
* Restored the property mapping required by Preact ISO minified builds, keeping runtime access reliable.
* Adjusted unmount timing so passive effects now clean up according to intended v11 behavior.
* Preserved constructor metadata when copying virtual nodes, improving behavior in hardened JavaScript and frozen intrinsics environments.
* Tightened compatibility validation so boxed React element symbols are rejected.

## Upgrade context

This release candidate introduces no breaking changes. Adopting version `11.0.0-rc.0` provides smaller outputs, rendering updates, improved server rendered content handling, and compatibility fixes.
See [PR #5](https://github.com/joels-sandgarden/preact/pull/5) for the changes included in this release candidate.