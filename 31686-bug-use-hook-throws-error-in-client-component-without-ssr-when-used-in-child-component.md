# Bug: `use` hook throws error in Client Component without SSR when used in child component

> Issue #31686 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31686

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0

## Steps To Reproduce

When using the `use` hook with a Promise context in a child component, it throws an error about async/await not being supported in Client Components. However, the same pattern works in the parent component.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

## Environment
- React version: 19.0.0
- Build tool: Vite
- No SSR implementation

```tsx
import { createContext, use, useState } from "react";
import "./App.css";

const AppCtx = createContext(new Promise<string>((r) => r("React")));

const Child = () => {
  const value = use(AppCtx);
  return <>{use(value)}</>;
};

function App() {
  const [value] = useState(new Promise<string>((r) => r("React")));
  return (
    <AppCtx value={value}>
      Hello
      <Child />
    </AppCtx>
  );
}

export default App;
```

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Uncaught Error: async/await is not yet supported in Client Components, only Server Components. This error is often caused by accidentally adding 'use client' to a module that was originally written for the server.

## The expected behavior

Since this is a client-side only application without any SSR, the `use` hook should work consistently in both parent and child components when handling Promise contexts.

