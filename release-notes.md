# v11.0.0-rc.0: Bundle size reductions and diffing improvements

## Version

`11.0.0-rc.0`

## Summary

This release candidate reduces compressed and bundled output sizes while improving rendering, hydration, and keyed list updates. It also strengthens vnode compatibility and adjusts effect cleanup behavior for more reliable runtime operation.

## Enhancements

* Improved rendering updates so keyed lists reorder more efficiently and preserve correct item placement.
* Enhanced hydration handling so excess markers no longer interfere with the resulting rendered tree.
* Refined ref application and guarded runtime checks to make rendering updates more consistent.

## Bug Fixes

* Corrected vnode cloning to retain the constructor, preventing runtime errors in hardened JavaScript environments.
* Deferred passive effect cleanup during unmount so cleanup runs at the intended stage of component removal.
* Restored `_bits` property mangling for the Preact ISO target to preserve compact generated output.
* Rejected boxed React element symbols during compatibility validation so invalid element values fail consistently.
* Streamlined insertion and unmount processing to reduce unnecessary work during rendering updates.

## Performance

* Reduced minified core and bundled artifact sizes for more compact Preact distributions.

## Additional Changes

* Updated package metadata and the developer tools integration to identify version `11.0.0-rc.0` consistently.
