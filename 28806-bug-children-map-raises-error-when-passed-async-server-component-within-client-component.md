# Bug: `Children.map` raises error when passed async server component within client component

> Issue #28806 - Created on 4/10/2024

> Original URL: https://github.com/facebook/react/issues/28806

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 14.1.4

## Steps To Reproduce

1. In a Next.js app or another framework that uses React server components, create an async server component called `Child`
2. Create a client component called `Client` which accepts the `children` prop and returns `Children.map(children, (child) => child)`
3. Create a server component called `Parent`, and return `Child` inside `Client`


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/devbox/broken-water-4kktmz

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Raises `Error: Objects are not valid as a React child (found: object with keys {$$typeof, _payload, _init}). If you meant to render a collection of children, use an array instead.`

## The expected behavior
Returns an unresolved Promise representing the child.
