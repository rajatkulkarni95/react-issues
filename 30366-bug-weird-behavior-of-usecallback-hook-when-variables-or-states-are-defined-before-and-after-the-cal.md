# Bug: Weird Behavior of useCallback() hook When Variables or States Are defined before and after the Callback (ES5)

> Issue #30366 - Created on 7/18/2024

> Original URL: https://github.com/facebook/react/issues/30366

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 17.0.2

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

When using ES5 with React Hooks, defining one dependency above and another below `useCallback()` results in either partial updates or correct code execution (as if both dependencies are defined above). This inconsistent behavior disrupts the expected functionality of `useCallback()`, making it difficult to manage state updates reliably and leading to unpredictable results.

**The main question is why React exhibits this behavior when dependencies are defined in such a manner and what the implications of doing this might be for the application.**

Here’s a detailed explanation: [StackOverflow question](https://stackoverflow.com/questions/78753216/react-hooks-behavior-difference-when-using-variables-and-states-in-usecallback).

CodeSandBox link: https://codesandbox.io/p/sandbox/webpack-react-hooks-usage-before-defination-5y2gj9?file=%2FApp.js%3A16%2C14

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Broken code works 

## The expected behavior
It depends on the scenarios provided in the Stack Overflow question.
