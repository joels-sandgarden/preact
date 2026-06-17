# Devtools Integration

## Overview

Import `preact/devtools` to initialize the devtools bridge.

## `addHookName(value, name)`

Use `addHookName(value, name)` to attach a label to a value before returning it. The helper keeps the original value unchanged, forwards the label to `options._addHookName` when that callback exists, and lets custom hooks or wrapper helpers show readable labels in the devtools panel.

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