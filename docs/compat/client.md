# Client Root API

## Overview

`preact/compat/client` exposes a React 18 style client root API for mounting and hydrating a tree in a single container.

## `createRoot(container)`

Call `createRoot(container)` to create a root for an existing container element. The returned root object provides:

- `render(children)` to mount or update the tree in that container.
- `unmount()` to remove the tree from that container.

Call `render()` whenever the tree changes. Each call replaces the previous content with the latest `children`.

## `hydrateRoot(container, children)`

Call `hydrateRoot(container, children)` when the container already contains server rendered content. The function performs one hydration pass and then returns the same root object shape as `createRoot()`.

After hydration, call `render()` to update the tree and `unmount()` to clear it.

## Example

```jsx
import { createRoot } from 'preact/compat/client';

const container = document.getElementById('app');
const root = createRoot(container);

root.render(<App name="Ada" />);
root.render(<App name="Grace" />);
root.unmount();
```

Use `hydrateRoot()` for a container that already holds markup. Use `createRoot()` for a fresh mount.