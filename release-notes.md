# Preact v11.0.0-rc.0: Bundle size reductions and diffing improvements

**Date:** 2026-08-12

**Version:** `11.0.0-rc.0`

## Summary

This release delivers smaller minified build artifacts, more efficient keyed reordering, improved diffing and hydration behavior, and stronger compatibility in hardened JavaScript environments. It also aligns passive effect cleanup timing with v11 behavior and includes no breaking changes.

## Performance

* **Reduced** minified build artifact size by refining protected and private name compression and simplifying expressions across compatibility, hooks, and JSX runtime packages.
* **Lowered** overhead during keyed reorder diff passes by reusing child collections locally and refining sequence lookup behavior.