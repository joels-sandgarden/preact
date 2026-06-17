# Scheduler compatibility reference

This document describes `preact/compat/scheduler`, the compatibility reference for libraries that expect React scheduler APIs.

It does not provide cooperative scheduling. `unstable_runWithPriority` calls its callback synchronously, and `unstable_now` returns the current timestamp from `performance.now()`.

## Priority constants

- `unstable_ImmediatePriority` equals `1` and marks the highest priority work.
- `unstable_UserBlockingPriority` equals `2` and marks work that should finish quickly.
- `unstable_NormalPriority` equals `3` and marks standard work.
- `unstable_LowPriority` equals `4` and marks work that can wait.
- `unstable_IdlePriority` equals `5` and marks the least urgent work.

## API

`unstable_runWithPriority(priority, callback)` accepts a numeric priority and a callback. The priority value keeps compatibility with libraries that read the React scheduler API, and the callback runs immediately.

`unstable_now` returns a timestamp from `performance.now()`.

## Example

```js
import {
  unstable_NormalPriority,
  unstable_runWithPriority,
} from 'preact/compat/scheduler';

unstable_runWithPriority(unstable_NormalPriority, () => {
  syncWork();
});
```

This pattern lets a library use the same import shape.