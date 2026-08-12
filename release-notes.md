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
