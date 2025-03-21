# Bug: inconsistent type checking behaviour for useState

> Issue #31451 - Created on 11/7/2024

> Original URL: https://github.com/facebook/react/issues/31451

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. declare a useState that accept the type: `Record<number, Record<number, true>>` 
2. when trying to use the `setState` function that is returned by `useState`, the type checking is inconsistent between an object that's assigned to a `const` and assigning the object directly 


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
Here is a reproduction [link](https://codesandbox.io/p/sandbox/fv2njd)

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

`setState` does not complain. 

## The expected behavior

`setState` should complain about the `newState` type

