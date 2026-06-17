# Test Utilities

## Overview

This document covers `preact/test-utils`, which provides helpers for render and effect flushing during tests. `preact/compat/test-utils` exports the same module.

## `setupRerender()`

Call `setupRerender()` when a test needs direct control over queued renders. It replaces `options.debounceRendering` with a drain function for pending render work and returns a function that drains the queue on demand.

## `act(callback)`

Use `act(callback)` to run a sync or async test callback and flush rerenders and effects after the callback finishes. The function returns a `Promise` that resolves after the flush completes.

## `teardown()`

Call `teardown()` after each test. It restores `options.debounceRendering` and clears any pending test state left behind by earlier renders.

## Example

```js
import { h, Component, render } from 'preact';
import { act, teardown } from 'preact/test-utils';

class Counter extends Component {
	state = { count: 0 };

	increment = () => {
		this.setState(({ count }) => ({ count: count + 1 }));
	};

	render(_, { count }) {
		return <button onClick={this.increment}>{count}</button>;
	}
}

const container = document.createElement('div');

afterEach(() => {
	teardown();
	container.innerHTML = '';
});

it('flushes renders during a test sequence', async () => {
	await act(() => {
		render(<Counter />, container);
	});

	expect(container.textContent).toBe('0');

	await act(() => {
		container.querySelector('button').dispatchEvent(
			new MouseEvent('click', { bubbles: true })
		);
	});

	expect(container.textContent).toBe('1');
});
```