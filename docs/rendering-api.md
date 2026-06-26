# Rendering API

## Overview

The `preact` package exports `render` and `hydrate` from its rendering module.

## `render(vnode, parentDom)`

Use `render()` to mount or update a tree in a DOM parent.

- When `parentDom` equals `document`, the implementation targets `document.documentElement`.
- The module calls `options._root(vnode, parentDom)` when that hook exists.
- It stores the previous tree on `parentDom._children` and reuses that tree on later calls against the same node.
- It wraps the incoming node in `Fragment` before it calls `diff()`.
- It passes commit and ref queues into `diff()`, then calls `commitRoot()` after diffing finishes.

## `hydrate(vnode, parentDom)`

`hydrate()` marks the vnode with the internal hydration flag and then calls `render()`. It does not follow a separate render path.

## Behavior and guarantees

The browser tests cover these guarantees:

- `render()` works with `document` and writes into `document.documentElement`.
- `render()` also works in an alternative document, such as an iframe.
- `hydrate()` preserves existing DOM when the markup already matches the vnode tree.
- `hydrate()` skips comment nodes while it matches DOM nodes.
- `hydrate()` supports `Fragment` nodes, including a root `Fragment`.
- `hydrate()` attaches event handlers to existing DOM during hydration.
- `commitRoot()` flushes queued effects and ref callbacks after diffing.

## Examples

### Render into the document root

```js
import { Fragment, render } from 'preact';

render(
  <Fragment>
    <head>
      <title>Test</title>
    </head>
    <body>
      <p>Test</p>
    </body>
  </Fragment>,
  document
);
```

### Hydrate existing DOM

```js
import { hydrate } from 'preact';

const save = () => {};

document.body.innerHTML = '<button>Save</button>';

hydrate(<button onClick={save}>Save</button>, document.body);
```