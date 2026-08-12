# 11.0.0-rc.0: bundle size reductions and diffing improvements

2026-08-12

Version `11.0.0-rc.0`

This release reduces bundle size, improves diffing and hydration behavior, and tightens compatibility across hooks and hardened JavaScript environments.

## Performance
* Improved bundle size across core, compat, hooks, and `jsx-runtime`.
* Restored `_bits` mangling for the Preact ISO build target while keeping the surrounding size reduction aliases in place.

## Bug Fixes
* Refined keyed reordering in diffing so child lookups stay efficient and the bounded longest increasing subsequence search remains accurate.
* Enhanced diffing and hydration so excess markers are handled more consistently and refs apply more simply.