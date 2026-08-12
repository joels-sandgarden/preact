# 11.0.0-rc.0: bundle size reductions and diffing improvements

2026-08-12

Version `11.0.0-rc.0`

This release delivers smaller bundles, steadier diffing, and compatibility refinements across hooks and hardened JavaScript environments.

## Performance
* Reduced bundle size across core, compat, hooks, and `jsx-runtime`.
* Restored `_bits` mangling for the Preact ISO build target while keeping the surrounding size reduction aliases.

## Bug Fixes
* Refined keyed reordering in diffing so child lookups stay efficient and the bounded longest increasing subsequence search stays accurate.
* Simplified diffing and hydration so excess markers are handled more consistently and refs apply more cleanly.
* Fixed vnode cloning in hardened JavaScript and frozen intrinsics environments by preserving `constructor` during clone operations.
* Adjusted hook cleanup timing so unmount and effect cleanup happen at the expected point in the lifecycle.
* Rejected a boxed React element symbol in compat to match the expected vnode shape.

## Additional Changes
* Synchronized package metadata and devtools versioning with `11.0.0-rc.0`.