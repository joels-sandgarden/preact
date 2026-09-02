# v1.0.2-test

* Reduced the size of compressed and minified artifacts.
* Optimized keyed reorder diffing while retaining a bounded longest increasing subsequence lookup.
* Improved correctness during hydration and diffing.
* Restored Preact ISO's `_bits` property mapping.
* Passive effect cleanup is deferred until unmount.
* VNode clones preserve constructors in hardened JavaScript environments.
* Compat validates elements with boxed React symbols more strictly.