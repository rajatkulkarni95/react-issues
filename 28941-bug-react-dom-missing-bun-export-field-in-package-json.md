# Bug [React-DOM]: Missing "bun" export field in package.json

> Issue #28941 - Created on 4/28/2024

> Original URL: https://github.com/facebook/react/issues/28941

## Description

In the exports field of the `react-dom`'s package.json, there is no "bun" field. Bun defaults to the "default" field for compatibility. However, the `./server.node.js` file doesn't export `renderToReadableStream()`, while Bun supports Web Streams out of the box.

See: [The Bun doc on Module resolution](https://bun.sh/docs/runtime/modules#importing-packages)
This issue is similar to #26906, but Bun always supported Web Streams so there is no backwards compatibility issues.

React version: 18.3.1

## Steps To Reproduce

1. Install `react-dom`.
2. Import `renderToReadableStream()`
3. Run the file using Bun
4. Notice that the error is something like this: `SyntaxError: Export named 'renderToReadableStream' not found in module '~/??/node_modules/react-dom/server.node.js'.`, which clearly shows that Bun uses the default export.

Link to code example:
I am not sure how to use Bun on the browser.

## The current behavior

Bun uses the default export. (aka server.node.js)

## The expected behavior

Bun uses a custom "bun" export. (aka server.browser.js)

I have tested the following change locally and it completely fixes this issue:

![fixed package.json](https://github.com/facebook/react/assets/36936511/08a9d496-edaf-48eb-9d41-e07c1b00a084)
