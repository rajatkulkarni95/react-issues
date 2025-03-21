# [React 19] Inconsistent "cache" api with Async Operations in react-server

> Issue #29955 - Created on 6/20/2024

> Original URL: https://github.com/facebook/react/issues/29955

## Description

**Description:**

When running the provided code with `node`, I encounter an issue where the cache is inconsistent depending on whether an async operation is present.

**Steps to Reproduce:**

1. Run the following code with `node`:

```typescript
const { renderToReadableStream } = require("react-server-dom-webpack/server.edge");
const { cache, createElement } = require("react");

const getId = cache(() => ({ id: Math.random() }));

const A = async () => {
    await new Promise(setImmediate);
    const id = getId();
    console.log(id);
    return null;
};

const B = async () => {
    const id = getId();
    console.log(id);
    return createElement(A, {}, null);
};

renderToReadableStream(createElement(B, {}, null), null);
```

2. Observe the console output. The `id` values logged in `A` and `B` are different.
3. Modify the code to remove the `await new Promise(setImmediate);` line from `A`:

```typescript
const A = async () => {
  const id = getId();
  console.log(id);
  return null;
};
```

4. Run the modified code with `node` again.
5. Observe the console output. The `id` values logged in `A` and `B` are now the same.

**Expected Behavior:**

The `id` values should be consistent regardless of the presence of async operations during the render.

**Actual Behavior:**

The `id` values are different when an async operation is present in the render method.

**Reproduction Code:**

You can run the code using the following command:

```
npm run start
```

or a codesandbox: https://codesandbox.io/p/github/nestarz/react-19-cache-issue/main?import=true
and the github repo: https://github.com/nestarz/react-19-cache-issue

**Additional Information:**

It seems there might be an issue with the request context propagation when async operations are involved during the render process. This leads to inconsistent behavior which could cause unpredictable bugs.

**Environment:**
- `node` v20.8.1
```json
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node --conditions react-server index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "react": "^19.0.0-rc-e684ca66ab-20240619",
    "react-server-dom-webpack": "^19.0.0-rc-e684ca66ab-20240619"
  }
}
```

It impacts the consistency and reliability of cache in async rendering scenarios, and it's critical when used as an alternative to server context, is this normal ? Thank you!
