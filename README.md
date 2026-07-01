> [!NOTE]
> This is the branch for the upcoming release, for patches to v10 you need the [v10.x branch](https://github.com/preactjs/preact/tree/v10.x)

<p align="center">
<a href="https://preactjs.com" target="_blank">

![Preact](https://raw.githubusercontent.com/preactjs/preact/8b0bcc927995c188eca83cba30fbc83491cc0b2f/logo.svg?sanitize=true 'Preact')

</a>
</p>
<p align="center">Fast <b>4kB</b> alternative to React with the same modern API.</p>

**All the power of Virtual DOM components, without the overhead:**

- Familiar React API & patterns: ES6 Class, hooks, and Functional Components
- Extensive React compatibility via a simple [preact/compat] alias
- Everything you need: JSX, <abbr title="Virtual DOM">VDOM</abbr>, [DevTools], <abbr title="Hot Module Replacement">HMR</abbr>, <abbr title="Server-Side Rendering">SSR</abbr>.
- Highly optimized diff algorithm and seamless hydration from Server Side Rendering
- Supports all modern browsers
- Transparent asynchronous rendering with a pluggable scheduler

### 💁 More information at the [Preact Website ➞](https://preactjs.com)

<table border="0">
<tbody>
<tr>
<td>

[![npm](https://img.shields.io/npm/v/preact.svg)](https://www.npmjs.com/package/preact)
[![Preact Slack Community](https://img.shields.io/badge/Slack%20Community-preact.slack.com-blue)](https://chat.preactjs.com)
[![OpenCollective Backers](https://opencollective.com/preact/backers/badge.svg)](#backers)
[![OpenCollective Sponsors](https://opencollective.com/preact/sponsors/badge.svg)](#sponsors)

[![coveralls](https://img.shields.io/coveralls/preactjs/preact/main.svg)](https://coveralls.io/github/preactjs/preact)
[![gzip size](https://img.badgesize.io/https://unpkg.com/preact/dist/preact.min.js?compression=gzip&label=gzip)](https://unpkg.com/preact/dist/preact.min.js)
[![brotli size](https://img.badgesize.io/https://unpkg.com/preact/dist/preact.min.js?compression=brotli&label=brotli)](https://unpkg.com/preact/dist/preact.min.js)

</td>
</tr>
</tbody>
</table>

You can find some awesome libraries in the [awesome-preact list](https://github.com/preactjs/awesome-preact) :sunglasses:

---

## Getting Started

> 💁 _**Note:** You [don't need ES2015 to use Preact](https://github.com/developit/preact-in-es3)... but give it a try!_

#### Tutorial: Building UI with Preact

With Preact, user interfaces begin as vnode trees. Components are functions or classes that return the tree they want to display. Those trees usually come from [JSX](https://react.dev/learn/writing-markup-with-jsx) (shown underneath) or [HTM](https://github.com/developit/htm), which uses standard JavaScript tagged templates. Both syntaxes describe elements, their props, and their children.

`render()` takes that vnode tree and reconciles it with the container's previous tree. It keeps the last tree on the DOM node, compares the new tree against it, and updates only the parts that changed. That approach keeps the DOM stable while Preact walks the tree, reuses components when it can, creates new ones when it must, and prepares any work that needs to wait until commit time.

```js
import { h, render } from 'preact';
// Tells babel to use h for JSX. It's better to configure this globally.
// See https://babeljs.io/docs/en/babel-plugin-transform-react-jsx#usage
// In tsconfig you can specify this with the jsxFactory
/** @jsx h */

// create our tree and append it to document.body:
render(
	<main>
		<h1>Hello</h1>
	</main>,
	document.body
);

// update the tree in-place:
render(
	<main>
		<h1>Hello World!</h1>
	</main>,
	document.body
);
// ^ this second invocation of render(...) updates only the text inside the <h1>
```

The second call changes only `Hello` to `Hello World!`, so Preact keeps the surrounding DOM and patches the text node in place. That same reconciliation model scales to components, where each component owns a subtree and Preact diffs that subtree against the previous result.

#### How Preact renders

Preact follows a short three step flow: JSX or HTM produces a vnode tree, `render()` passes that tree into `diff()`, and `commitRoot()` flushes the queued work after reconciliation. During diffing, Preact creates a component when no previous instance exists, reuses an existing one when the types match, applies derived state, runs pre-render hooks, and lets `shouldComponentUpdate()` stop a render early when it returns `false`. Class components can also capture `getSnapshotBeforeUpdate()` before the DOM changes and extend context with `getChildContext()`.

Function components follow the same diffing path. If one of them marks itself dirty during render, Preact runs it again so the final tree stays in sync. `setState()` and `forceUpdate()` schedule rerenders through a queue, and Preact drains that queue in order so related updates stay consistent.

The diff stage also reconciles children, places or moves DOM nodes, and collects refs for later. `componentDidMount()`, `componentDidUpdate()`, refs, and queued render callbacks all flush in `commitRoot()` after reconciliation finishes.

The same pattern keeps larger component trees manageable. Each component can focus on its own subtree instead of recalculating the whole interface from scratch. Here's an example:

```js
import { render, h } from 'preact';
import { useState } from 'preact/hooks';

/** @jsx h */

const App = () => {
	const [input, setInput] = useState('');

	return (
		<div>
			<p>Do you agree to the statement: "Preact is awesome"?</p>
			<input value={input} onInput={e => setInput(e.target.value)} />
		</div>
	);
};

render(<App />, document.body);
```

---

## Sponsors

Become a sponsor and get your logo on our README on GitHub with a link to your site. [[Become a sponsor](https://opencollective.com/preact#sponsor)]

<a href="https://opencollective.com/preact/sponsor/0/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/1/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/2/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/3/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/4/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/4/avatar.svg"></a>
<a href="https://snyk.co/preact" target="_blank"><img src="https://res.cloudinary.com/snyk/image/upload/snyk-marketingui/brand-logos/wordmark-logo-color.svg" width="192" height="64"></a>
<a href="https://opencollective.com/preact/sponsor/5/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/6/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/7/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/8/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/9/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/9/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/10/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/10/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/11/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/11/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/12/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/12/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/13/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/13/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/14/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/14/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/15/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/15/avatar.svg"></a>
<a href="https://github.com/guardian" target="_blank"> &nbsp; &nbsp; &nbsp; <img src="https://github.com/guardian.png" width="64" height="64"> &nbsp; &nbsp; &nbsp; </a>
<a href="https://www.sent.dm" target="_blank"><img src="https://github.com/sentdm.png?size=64" alt="SentDM" width="64" height="64" hspace="96"></a>
<a href="https://www.songsterr.com/" target="_blank"><img src="https://github.com/songsterr.png?size=64" alt="Songsterr" width="64" height="64" hspace="96"></a>
<a href="https://deno.land" target="_blank"><img src="https://github.com/denoland.png?size=64" alt="Deno" width="64" height="64" hspace="96"></a>
<a href="https://opencollective.com/preact/sponsor/16/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/16/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/17/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/17/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/18/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/18/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/19/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/19/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/20/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/20/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/21/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/21/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/22/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/22/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/23/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/23/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/24/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/24/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/25/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/25/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/26/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/26/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/27/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/27/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/28/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/28/avatar.svg"></a>
<a href="https://opencollective.com/preact/sponsor/29/website" target="_blank"><img src="https://opencollective.com/preact/sponsor/29/avatar.svg"></a>

## Backers

Support us with a monthly donation and help us continue our activities. [[Become a backer](https://opencollective.com/preact#backer)]

<a href="https://opencollective.com/preact/backer/0/website" target="_blank"><img src="https://opencollective.com/preact/backer/0/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/1/website" target="_blank"><img src="https://opencollective.com/preact/backer/1/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/2/website" target="_blank"><img src="https://opencollective.com/preact/backer/2/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/3/website" target="_blank"><img src="https://opencollective.com/preact/backer/3/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/4/website" target="_blank"><img src="https://opencollective.com/preact/backer/4/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/5/website" target="_blank"><img src="https://opencollective.com/preact/backer/5/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/6/website" target="_blank"><img src="https://opencollective.com/preact/backer/6/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/7/website" target="_blank"><img src="https://opencollective.com/preact/backer/7/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/8/website" target="_blank"><img src="https://opencollective.com/preact/backer/8/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/9/website" target="_blank"><img src="https://opencollective.com/preact/backer/9/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/10/website" target="_blank"><img src="https://opencollective.com/preact/backer/10/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/11/website" target="_blank"><img src="https://opencollective.com/preact/backer/11/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/12/website" target="_blank"><img src="https://opencollective.com/preact/backer/12/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/13/website" target="_blank"><img src="https://opencollective.com/preact/backer/13/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/14/website" target="_blank"><img src="https://opencollective.com/preact/backer/14/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/15/website" target="_blank"><img src="https://opencollective.com/preact/backer/15/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/16/website" target="_blank"><img src="https://opencollective.com/preact/backer/16/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/17/website" target="_blank"><img src="https://opencollective.com/preact/backer/17/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/18/website" target="_blank"><img src="https://opencollective.com/preact/backer/18/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/19/website" target="_blank"><img src="https://opencollective.com/preact/backer/19/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/20/website" target="_blank"><img src="https://opencollective.com/preact/backer/20/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/21/website" target="_blank"><img src="https://opencollective.com/preact/backer/21/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/22/website" target="_blank"><img src="https://opencollective.com/preact/backer/22/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/23/website" target="_blank"><img src="https://opencollective.com/preact/backer/23/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/24/website" target="_blank"><img src="https://opencollective.com/preact/backer/24/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/25/website" target="_blank"><img src="https://opencollective.com/preact/backer/25/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/26/website" target="_blank"><img src="https://opencollective.com/preact/backer/26/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/27/website" target="_blank"><img src="https://opencollective.com/preact/backer/27/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/28/website" target="_blank"><img src="https://opencollective.com/preact/backer/28/avatar.svg"></a>
<a href="https://opencollective.com/preact/backer/29/website" target="_blank"><img src="https://opencollective.com/preact/backer/29/avatar.svg"></a>

---

## License

MIT

[![Preact](https://i.imgur.com/YqCHvEW.gif)](https://preactjs.com)

[preact/compat]: https://github.com/preactjs/preact/tree/main/compat
[hyperscript]: https://github.com/dominictarr/hyperscript
[DevTools]: https://github.com/preactjs/preact-devtools
