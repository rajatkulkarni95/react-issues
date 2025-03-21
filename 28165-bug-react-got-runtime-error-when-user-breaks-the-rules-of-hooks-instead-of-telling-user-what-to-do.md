# Bug: react got runtime error when user breaks the rules of hooks, instead of telling user what to do

> Issue #28165 - Created on 1/31/2024

> Original URL: https://github.com/facebook/react/issues/28165

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. Open the link below, it will show a page with a button.
2. Click the button, and you will get the error.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/a-react-hooks-edge-case-that-causes-react-crash-rddmkh?file=%2Fsrc%2FApp.js%3A1%2C1

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Users get a runtime error `Cannot read properties of undefined (reading 'length')`.

<img width="727" alt="image" src="https://github.com/facebook/react/assets/27483702/4fddd677-f60d-442f-8109-805b98f958b6">

This is because React uses different data structures in `memoizedState`, e.g. `object` for `useEffect`, `array` for `useCallback`. If users break the rules of hooks, the following code will crash, which will confuse users:

```ts
function updateCallback(callback, deps) {
  ...
    if (nextDeps !== null) {
      var prevDeps = prevState[1];                  // <- 1. prevState is now an object

      if (areHookInputsEqual(nextDeps, prevDeps)) { // <- 2. passes an undefined here
        return prevState[0];
      }
    }
  }
  ...
}

function areHookInputsEqual(nextDeps, prevDeps) {
  ...
    if (nextDeps.length !== prevDeps.length) {      // <- 3. this will crash - prevDeps is undefined
      error('The final argument passed to %s changed size between renders. The ' + 'order and size of this array must remain constant.\n\n' + 'Previous: %s\n' + 'Incoming: %s', currentHookNameInDev, "[" + prevDeps.join(', ') + "]", "[" + nextDeps.join(', ') + "]");
    }
  }
  ...
}
```

## The expected behavior

Users should receive a React message like other scenarios that break the rules of hooks (`Rendered more hooks than during the previous render.`).

Actually, if we modify the last hook from `useCallback` to `useEffect`, we can get this message.

<img width="562" alt="image" src="https://github.com/facebook/react/assets/27483702/8d37adfa-8993-4180-b5f5-f048c4964e0a">

ESLint can not identify this scenario and will not report errors. If it's not the responsibility of React, at least the `eslint-plugin-react` should detect it.
