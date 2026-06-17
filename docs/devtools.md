# Devtools Integration

## Overview

Import `preact/devtools` to initialize the devtools bridge. The module forwards custom hook names through `options._addHookName`, so custom hooks and wrapper helpers can show readable labels in the devtools panel.

## `addHookName(value, name)`

Use `addHookName(value, name)` to attach a label to a value before returning it. The helper keeps the original value unchanged and sends the label to the devtools bridge when the bridge exposes name support.

## Example

```js
import { addHookName } from 'preact/devtools';

function useLabeledState() {
	const state = useState(0);
	return addHookName(state, 'useLabeledState');
}

function withLabel(value) {
	return addHookName(value, 'custom helper value');
}
```

Import the entry point once so the bridge starts before custom hooks or helpers call `addHookName`.