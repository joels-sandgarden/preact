# v11.0.0-rc.0: Reduce bundle sizes and improve diffing

## Version

`11.0.0-rc.0`

## Summary

This release candidate makes rendering, existing markup handling, and component cleanup more reliable. It also strengthens compatibility checks and keeps release information aligned.

## Enhancements

* Improved list updates so items keep the correct positions when lists change.
* Enhanced rendering with existing markup so extra markers do not interfere with rendered content.
* Refined element reference handling and runtime safeguards so rendering updates behave consistently.

## Bug Fixes

* Corrected cloned virtual elements to retain constructor information, preventing runtime errors in hardened JavaScript environments.
* Deferred cleanup for passive effects during component removal so cleanup runs at the intended stage.
* Restored compact property naming for Preact ISO builds to preserve smaller generated output.
* Rejected React element symbols wrapped in objects during compatibility validation, so invalid values fail consistently.
* Streamlined insertion and component removal so rendering updates do less unnecessary work.

## Performance

* Reduced compressed core and bundled artifact sizes, making Preact distributions more compact.

## Additional Changes

* Updated package metadata and the developer tools integration to report version `11.0.0-rc.0` consistently.
