# Client Root API

## Overview

`preact/compat/client` exposes the React 18 style client root API for mounting or hydrating a tree in one container.

## `createRoot(container)`

Call `createRoot(container)` to create a root for an existing container element. The returned root object includes:

- `render(children)` to mount or update the tree in that container.
- `unmount()` to remove the tree from that container.

Call `render(children)` whenever the tree changes. Each call replaces the previous tree with the latest `children`.

## `hydrateRoot(container, children)`

Call `hydrateRoot(container, children)` when the container already contains server rendered content. It performs one hydration pass, then returns the same root object as `createRoot()`.

After hydration, call `render(children)` to update the tree and `unmount()` to clear it.

## Example

```jsx
import { createRoot } from 'preact/compat/client';

const container = document.getElementById('app');
const root = createRoot(container);

root.render(<App name="Ada" />);
root.render(<App name="Grace" />);
root.unmount();
```
