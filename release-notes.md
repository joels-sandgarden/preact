# Preact v11.0.0-rc.0: Bundle size reductions and diffing improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

## Summary

This release delivers smaller compressed build artifacts, more efficient list reordering, more reliable updates for server-rendered content, and stronger compatibility when JavaScript built-ins are restricted. It also aligns cleanup after rendering with v11 behavior and includes no breaking changes.

## Performance

* **Reduced** compressed build artifact size by shortening internal names and simplifying expressions across compatibility, hooks, and JSX runtime packages.
* **Lowered** overhead while reordering keyed lists by reusing existing child data and refining the ordering process.

## Rendering and server-rendered content

* **Improved** handling of extra markers while attaching server-rendered content so they no longer disrupt updates.
* **Simplified** how the framework applies element references during root updates to keep references consistent.
* **Streamlined** rendering checks to improve correctness in edge cases.

## Compatibility

* **Restored** the expected compressed property mapping in Preact ISO builds, keeping the internal bit field available as expected.
* **Deferred** cleanup after rendering during unmount to match v11 timing.
* **Strengthened** element copying in environments that freeze JavaScript built-ins while preserving required object metadata.
* **Corrected** compatibility validation to reject React element symbols wrapped in objects rather than accept them as valid elements.

## Additional changes

* **Updated** package and development tooling version identifiers to `11.0.0-rc.0`.