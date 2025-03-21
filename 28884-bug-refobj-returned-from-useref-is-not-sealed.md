# Bug: refObj returned from useRef is not sealed

> Issue #28884 - Created on 4/20/2024

> Original URL: https://github.com/facebook/react/issues/28884

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: ^18.0.0

## Steps To Reproduce

1. Create a ref using `useRef`.
2. Trying to delete the current property or add a new property.
![image](https://github.com/facebook/react/assets/64327685/58ff4877-8d3a-479f-8010-e3fd558de36a)

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/funny-sid-pm6xzq?file=%2Fsrc%2FApp.js%3A12%2C41

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
The current property is deleted, and a new property is added when trying to add it to the ref Object

## The expected behavior
ref Object is sealed, so we should only be allowed to change its current value but not being able to delete it or add a new property to the object.


both `createRef` and `useRef` are sealed but only the ref object returned from `createRef` is selaed:

useRef:mountRef : [link](https://github.com/facebook/react/blob/6faf6f5/packages/react-reconciler/src/ReactFiberHooks.js#L907-L920)

createRef: [Link](https://github.com/facebook/react/blob/0061ca6cf47c5124d2ebe708481fb03da9e8e267/packages/react/src/ReactCreateRef.js#L12)

