 # v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Version

`11.0.0-rc.0`

## Summary

This release candidate delivers smaller compressed builds, more efficient keyed updates, and improved rendering correctness. It also updates the package version and DevTools attachment for `11.0.0-rc.0`.

## Improvements

* Reduced compressed and bundled output sizes through more efficient minification across Preact, hooks, JSX runtime, and compatibility builds.
* Improved keyed list reordering with more efficient diffing and bounded longest increasing subsequence calculations.
* Corrected hydration and rendering edge cases so excess hydration markers, references, and guarded updates behave more reliably.