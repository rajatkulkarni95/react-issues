# Bug: Input don't send "select" events when type is "email"

> Issue #31156 - Created on 10/9/2024

> Original URL: https://github.com/facebook/react/issues/31156

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: reproduced on 17 and 18

## Steps To Reproduce

1. Create an input like this: `<input text="move the selection around" onSelect={console.log} type="email" />`
2. Move the selection around and see that onSelect is emitted only on focus and blur. Notice that you get normal behavior if you remove the type

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

https://codesandbox.io/p/sandbox/recursing-kilby-z6h9dz?file=%2Fsrc%2FApp.js%3A15%2C1

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Does not emit "select" events

## The expected behavior

Should emit the "select" events
