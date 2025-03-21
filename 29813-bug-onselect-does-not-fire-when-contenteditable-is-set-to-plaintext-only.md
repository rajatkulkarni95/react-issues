# Bug: onSelect does not fire when contentEditable is set to "plaintext-only"

> Issue #29813 - Created on 6/8/2024

> Original URL: https://github.com/facebook/react/issues/29813

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18

## Steps To Reproduce

1. Create a `div` with `contentEditable="plaintext-only".
2. Define an `onSelect` event handler.
3. It does not fire upon interacting with the `div`.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/unruffled-kapitsa-9rv7z5

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
`onSelect` does not fire when `contentEditable` is set to `plaintext-only` but fires when it is set to `true`.

## The expected behavior
`onSelect` should fire for both cases.
