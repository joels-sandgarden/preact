# v1.0.2-test

### Bug Fixes

* Reduce compressed core size and lower processing overhead when keyed items change order while keeping lookup work bounded.
* Improve rendering correctness when server rendered output contains excess markers and when references update.
* Correct internal property mapping in Preact ISO builds.
* Defer passive effect cleanup during unmount to provide the intended v11 timing.
* Preserve component type information when cloning rendered elements in hardened JavaScript environments.
* Reject invalid boxed React element identifiers for improved compatibility.
* Reduce expression size in compatibility and JSX runtime packages.
* Update package metadata and the developer tools integration to `11.0.0-rc.0`.

This release introduces no breaking changes.