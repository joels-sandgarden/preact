# Preact v11.0.0-rc.0: Bundle size reductions and diffing improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

## Summary

This release delivers smaller minified build artifacts, more efficient keyed reordering, improved diffing and hydration behavior, and stronger compatibility in hardened JavaScript environments. It also aligns passive effect cleanup timing with v11 behavior and includes no breaking changes.

## Performance

* **Reduced** minified build artifact size by refining protected and private name compression and simplifying expressions across compatibility, hooks, and JSX runtime packages.
* **Lowered** overhead during keyed reorder diff passes by reusing child collections locally and refining sequence lookup behavior.

## Rendering and hydration

* **Improved** hydration handling for excess markers so additional markers no longer disrupt reconciliation.
* **Simplified** ref application during root updates for more consistent rendered references.
* **Streamlined** guarded rendering checks to improve correctness in edge cases.

## Compatibility

* **Restored** the expected minified property mapping for the Preact ISO build so its internal bit field remains accessible.
* **Deferred** passive effect cleanup during unmount to match the intended v11 timing.
* **Strengthened** element cloning in hardened JavaScript and frozen intrinsic environments by preserving required object metadata.
* **Corrected** compatibility validation to reject boxed React element symbols instead of accepting them as valid elements.

## Additional changes

* **Updated** package and development tooling version identifiers to `11.0.0-rc.0`.