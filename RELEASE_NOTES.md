# v11.0.0-rc.0: Bundle size and diffing improvements

**Date:** 2026-08-12

**Version:** 11.0.0-rc.0

## Summary

This release reduces generated output sizes and improves how Preact updates keyed lists, hydrated content, references, and lifecycle effects. It also strengthens compatibility behavior in hardened environments and adds stricter React element validation.

## Performance

* Reduced compressed and bundled output sizes across the core, compat, hooks, and JSX runtime packages by shortening repeated property names and simplifying generated expressions.

* Restored `_bits` compression for Preact ISO builds, reducing their generated output size.

## Enhancements

* Improved keyed list reordering by reusing item data and refining sequence lookup, reducing unnecessary updates when items change position.

* Improved hydration to handle excess markers more reliably and made refs behave consistently while Preact commits rendered content.

## Bug Fixes

* Deferred cleanup for passive effects until after unmount processing completes, preserving expected timing for hooks.

* Preserved virtual node constructors when cloning nodes in hardened environments, including environments with frozen built-ins.

## Additional Changes

* Strengthened compatibility validation so boxed React element symbols no longer pass as valid React elements.

* Acknowledged joel-solymosi for making a first contribution to Preact.
