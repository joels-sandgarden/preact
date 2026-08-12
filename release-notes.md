# v11.0.0-rc.0: Reduce Bundle Size and Improve Diffing

This release candidate reduces compressed and bundled output size while improving keyed reordering, hydration, compatibility, and unmount behavior. It does not introduce breaking changes.

## Performance

* Reduced compressed and bundled output size through more efficient code naming.
* Restored compact names for Preact ISO output to preserve its smaller file size.
* Improved updates that reorder keyed elements, reducing processing overhead.
* Refined the ordering search used for keyed updates to improve correctness.
* Simplified insertion and unmount processing for more consistent updates.

## Bug Fixes

* Corrected hydration handling when the rendered output contains excess markers.
* Fixed element cloning in hardened JavaScript environments by retaining the constructor.
* Adjusted passive effect cleanup to run at the correct time during unmounting.
* Streamlined element reference updates and protected update checks to improve reliability.
* Enhanced compatibility validation for React elements that use boxed symbols.

## Additional Changes

* Updated `package.json`, `package-lock.json`, and the development tools attachment to report version `11.0.0-rc.0`.