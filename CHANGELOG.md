# v1.0.2-test

* Reduced the size of compressed and minified artifacts.
* Optimized keyed reorder diffing while retaining a bounded longest increasing subsequence lookup.
* Improved correctness during hydration and diffing.
* Restored Preact ISO's `_bits` property mapping.
* Deferred passive effect cleanup until unmount.
* Preserved constructors when cloning VNodes in hardened JavaScript environments.
* Strengthened compat element validation for boxed React symbols.