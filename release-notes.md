# Preact v11.0.0-rc.0: Bundle size reductions and diffing improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

## Summary

This release delivers smaller compressed build artifacts, more efficient keyed list reordering, more reliable handling of server rendered content, and stronger compatibility in JavaScript environments that restrict built-in objects. It also aligns cleanup after rendering with v11 behavior and includes no breaking changes.

## Performance

* **Reduced** compressed build artifact size by shortening internal names and simplifying expressions across compatibility, hooks, and JSX runtime packages.
* **Lowered** overhead during keyed list reordering by reusing existing child data and refining the ordering process.

## Rendering and hydration

* **Improved** handling of extra markers while attaching server rendered content so they no longer disrupt updates.
* **Simplified** element reference application during root updates for more consistent rendered references.
* **Streamlined** rendering checks to improve correctness in edge cases.

## Compatibility

* **Restored** the expected compressed property mapping for Preact ISO builds so the expected internal field remains accessible.
* **Deferred** cleanup after rendering during unmount to match the intended v11 timing.
* **Strengthened** element copying in JavaScript environments that freeze built-in objects by preserving required object metadata.
* **Corrected** compatibility validation to reject React element symbols wrapped in objects instead of accepting them as valid elements.

## Additional changes

* **Updated** package and development tooling version identifiers to `11.0.0-rc.0`.