# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

Date: 2026-08-12

Version: `v11.0.0-rc.0`

This release candidate reduces output size and improves rendering, hydration, compatibility, and effect cleanup behavior across Preact.

## Bundle Size

* Reduced the compressed size of the Preact core while preserving efficient lookup during list reordering.
* Decreased bundled output across core rendering, compatibility, hooks, and JSX runtime packages through targeted simplifications.