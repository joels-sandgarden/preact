# `preact/compat/server`

## Overview

This document describes the `preact/compat/server` entry point for server rendering. The module delegates string rendering to `preact-render-to-string` and streaming output to its stream helpers. The browser fallback at `preact/compat/server.browser` exposes only the string rendering helpers.

## Prerequisites

- `preact-render-to-string` must be available at runtime.
- `preact-render-to-string` must be version `6.5.0` or later when code uses `renderToPipeableStream` or `renderToReadableStream`.

## Server rendering helpers

### `renderToString`

Use `renderToString` to convert a Preact tree into an HTML string.

### `renderToStaticMarkup`

`renderToStaticMarkup` aliases `renderToString`, so both functions return the same output.

### `renderToPipeableStream`

Use `renderToPipeableStream` for Node output that writes to a pipeable stream. The compat entry point loads this helper from `preact-render-to-string/stream-node`.

### `renderToReadableStream`

Use `renderToReadableStream` for environments that consume a `ReadableStream`. The compat entry point loads this helper from `preact-render-to-string/stream`.

## Browser fallback

`preact/compat/server.browser` exports `renderToString` and `renderToStaticMarkup` only. It does not expose the streaming helpers.

## Examples

### Render HTML as a string

```js
import { h } from 'preact';
import { renderToString } from 'preact/compat/server';

const html = renderToString(<h1>Hello</h1>);
```

### Stream HTML from Node

```js
import { h } from 'preact';
import { renderToPipeableStream } from 'preact/compat/server';

const stream = renderToPipeableStream(<h1>Hello</h1>);
stream.pipe(process.stdout);
```

## Troubleshooting

- `renderToString()` reports a missing dependency when `preact-render-to-string` is not installed in the runtime.
- `renderToPipeableStream()` and `renderToReadableStream()` report a version update error when `preact-render-to-string` is older than `6.5.0`.