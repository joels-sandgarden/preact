 # v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

This release candidate reduces compressed and bundled output size while improving keyed reordering, hydration, compatibility, and unmount behavior. It does not introduce breaking changes.

## Performance

* Reduced compressed and bundled output size through updated minification settings.
* Restored compact naming for the Preact ISO target to preserve its smaller output.
* Improved keyed reorder diff passes to reduce processing overhead.
* Refined the search used during keyed reordering to improve update correctness.
* Simplified insertion and unmount processing for more consistent updates.

## Bug Fixes

* Corrected hydration handling when the rendered output contains excess markers.
* Fixed vnode cloning in hardened JavaScript environments by retaining the constructor.
* Adjusted passive effect cleanup to run at the correct time during unmounting.
* Streamlined ref application and guarded diff checks to improve update reliability.
* Enhanced compatibility validation for boxed React element symbols.

## Additional Changes

* Updated package metadata and the development tools integration to report version `11.0.0-rc.0`.