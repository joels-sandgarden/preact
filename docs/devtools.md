# Devtools Integration

## Overview

Import `preact/devtools` to initialize the devtools bridge.

## `addHookName(value, name)`

Use `addHookName(value, name)` to attach a label to a value before returning it. The helper keeps the original value unchanged and forwards the label to `options._addHookName` when that callback exists.

Custom hooks and wrapper helpers can use this function to show readable labels in the devtools panel.

## Example

```js
import { useState } from 'preact/hooks';
import { addHookName } from 'preact/devtools';

function useLabeledState() {
	const state = useState(0);
	return addHookName(state, 'useLabeledState');
}

function withUserLabel(value) {
	return addHookName(value, 'user data');
}
```

Import the entry point once before custom hooks or helpers call `addHookName`.