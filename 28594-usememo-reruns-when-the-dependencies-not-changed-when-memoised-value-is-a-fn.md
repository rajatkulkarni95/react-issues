# useMemo reruns when the dependencies not changed when memoised value is a fn

> Issue #28594 - Created on 3/20/2024

> Original URL: https://github.com/facebook/react/issues/28594

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18

Please refer the codesandbox link 
https://codesandbox.io/p/sandbox/react-dev-forked-8whdhd?file=%2Fsrc%2FTodoList.js%3A25%2C11

## Steps To Reproduce

useMemo reruns when the dependencies not changed when returned value is anonymous function.

Link to code example:

https://codesandbox.io/p/sandbox/react-dev-forked-8whdhd?file=%2Fsrc%2FTodoList.js%3A25%2C11

## The current behavior
memoised fn re renders.

## The expected behavior
memoised fn not to re render.
