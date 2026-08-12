# v11.0.0-rc.0: Reduce bundle sizes and improve diffing

## Version

`11.0.0-rc.0`

## Summary

This release candidate makes Preact distributions smaller and keeps rendering, hydration, and component cleanup behavior more reliable. It also strengthens compatibility checks and version alignment.

## Enhancements

* Improved list updates so items keep the correct positions when lists with stable identifiers change.
* Enhanced hydration so extra markers do not interfere with rendered content.
* Refined element reference handling and runtime safeguards so rendering updates behave consistently.

## Bug Fixes

* Corrected virtual node cloning to retain its constructor, preventing runtime errors in hardened JavaScript environments.
* Deferred passive effect cleanup during component removal so cleanup runs at the intended stage.
* Restored compact `_bits` naming for Preact ISO builds to preserve smaller generated output.
* Rejected React element symbols wrapped in objects during compatibility validation, so invalid values fail consistently.
* Streamlined insertion and component removal so rendering updates do less unnecessary work.

## Performance

* Reduced minified core and bundled artifact sizes, making Preact distributions more compact.

## Additional Changes

* Updated package metadata and the developer tools integration to report version `11.0.0-rc.0` consistently.
