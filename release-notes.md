# v11.0.0-rc.0: Bundle Size Reductions and Diffing Improvements

Date: 2026-08-12

Version: `v11.0.0-rc.0`

This release candidate makes Preact smaller and improves how it updates page content, works with existing markup, handles integrations, and cleans up effects.

## Bundle Size

* Reduced the minified Preact core size while retaining bounded lookup for reordered item lists.
* Decreased bundle size across Preact's core, compatibility, hooks, and JSX runtime packages through targeted simplifications.

## Rendering and Diffing

* Improved reordering for keyed item lists to reduce work when children change.
* Enhanced handling of extra markers when attaching to existing page content.
* Simplified how element references are applied during rendering.
* Refined rendering checks to improve how Preact compares and updates content.

## Compatibility and Correctness

* Corrected the `_bits` internal property mapping used by Preact ISO builds.
* Adjusted passive effect cleanup timing during unmounts for the intended v11 behavior.
* Strengthened virtual node cloning in hardened JavaScript environments by preserving constructor information.
* Expanded compatibility checks for React elements represented by boxed symbols.

## Release Metadata

* Updated package and developer tools version metadata to `11.0.0-rc.0`.
* Confirmed no breaking changes for this release candidate.