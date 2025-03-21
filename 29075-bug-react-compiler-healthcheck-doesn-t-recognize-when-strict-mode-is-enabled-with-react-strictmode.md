# Bug: `react-compiler-healthcheck` doesn't recognize when strict mode is enabled with `<React.StrictMode />`

> Issue #29075 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29075

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. Create a react application
2. Use `<React.StrictMode />` to enable strict mode (instead of `<StrictMode />`
3. Run `npx react-compiler-healthcheck`:
    
    ```sh
    ❯ npx react-compiler-healthcheck
    Successfully compiled 1 out of 1 components.
    StrictMode usage not found.
    Found no usage of incompatible libraries.
    ```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

This repo was created by running `pnpm create vite` and selecting React with Typescript. No changes were made to the code.

https://github.com/psychedelicious/react-compiler-healthcheck_strict-mode

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

The health check doesn't recognize when strict mode is enabled with `<React.StrictMode />`.

## The expected behavior

The health check recognizes when strict mode is enabled with `<React.StrictMode />`.
