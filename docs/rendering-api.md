# Rendering API

## Overview

The `preact` package exports `render` and `hydrate` from the rendering module. Both functions accept a virtual node and a DOM parent, and both follow the package level API from `preact`.

## `render(vnode, parentDom)`

`render()` accepts a virtual node and a DOM element.

- When `parentDom` equals `document`, the implementation targets `document.documentElement`.
- Before diffing, the module calls `options._root(vnode, parentDom)` when that hook exists.
- The implementation stores the previous tree on `parentDom._children`, then reuses that tree on later calls against the same DOM node.
- It wraps the incoming node in `Fragment` before it calls `diff()`.
- It passes commit and ref queues into `diff()`, then calls `commitRoot()` to flush queued work after diffing finishes.

## `hydrate(vnode, parentDom)`

`hydrate()` marks the vnode with the internal hydration flag and then calls `render()`. It does not follow a separate render path.

## Behavior and guarantees

The browser tests cover these behaviors:

- `render()` works with `document` and writes into `document.documentElement`.
- `render()` also works in an alternative document, such as an iframe.
- `hydrate()` preserves existing DOM when the markup already matches the vnode tree.
- `hydrate()` skips comment nodes while it matches DOM nodes.
- `hydrate()` supports `Fragment` nodes, including a root `Fragment`.
- `hydrate()` attaches event handlers to existing DOM during hydration.
- `render()` and `hydrate()` flush queued effects and ref callbacks after diffing.

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