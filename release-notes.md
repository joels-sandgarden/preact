# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

Date: 2026-08-12

Version: `v11.0.0-rc.0`

This release candidate makes Preact smaller and improves how it updates page content, works with existing markup, handles integrations, and cleans up effects.

## Bundle Size

* Reduced minified Preact core size while retaining bounded lookup for reordered item lists.
* Decreased bundle size across Preact's core, compatibility, hooks, and JSX runtime packages through targeted simplifications.

## Rendering and Diffing

* Improved reordering of keyed items to reduce work when child lists change.
* Enhanced handling of extra markers when attaching to existing page content.
* Simplified application of element references during rendering.
* Refined rendering checks to improve how Preact compares and updates content.

## Compatibility and Correctness

* Restored the `_bits` internal property mapping used by Preact ISO builds.
* Deferred cleanup for passive effects during unmounts to provide the intended v11 timing.
* Preserved constructor information when cloning virtual nodes in hardened JavaScript environments.
* Added compatibility validation for React elements represented by boxed symbols.

## Release Metadata

* Updated package and developer tools version metadata to `11.0.0-rc.0`.
* Confirmed no breaking changes for this release candidate.