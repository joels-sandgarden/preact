# v11.0.0-rc.0 — bundle size reductions and diffing improvements

Date: 2026-08-12  
Version: `11.0.0-rc.0`

This release focuses on smaller distributable output, keyed reorder diffing refinements, hydration handling improvements, effect cleanup timing updates, VNode cloning compatibility fixes, and compat validation corrections.

## New Features
* Updated the release line to `11.0.0-rc.0` across the published package metadata and development tooling.

## Performance
* Improved compressed and bundled output by tightening property mangling in `mangle.json` and simplifying expressions across `compat`, `hooks`, and `jsx-runtime`.
* Refined keyed reorder diffing by hoisting the child array locally and adjusting the LIS and bounded-LIS search used during reorder handling.

## Bug Fixes
* Enhanced hydration excess-marker handling in `src/diff/index.js` and streamlined related diffing checks for server-rendered updates.