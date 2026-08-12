 # v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

## Version

`11.0.0-rc.0`

## Summary

This release candidate ships smaller compressed builds, faster keyed updates, and more reliable rendering. The package version and DevTools attachment now identify `11.0.0-rc.0`.

## Improvements

* Reduced compressed and bundled output sizes with smaller minified code across Preact, hooks, JSX runtime, and compatibility builds.
* Improved keyed list reordering with lower diffing overhead while preserving the bounded LIS optimization.
* Corrected hydration and rendering edge cases so excess hydration markers, references, and guarded updates behave reliably.
* Restored `_bits` mangling for the Preact ISO target so minified builds read the expected internal field.
* Deferred passive effect cleanup during unmount to match the intended v11 behavior.
* Hardened VNode cloning for frozen or restricted JavaScript environments by retaining the VNode constructor in each clone.
* Fixed compatibility validation so boxed React element symbols are rejected consistently.