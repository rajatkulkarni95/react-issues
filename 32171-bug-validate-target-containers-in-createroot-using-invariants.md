# Bug: Validate Target Containers in createRoot() Using Invariants

> Issue #32171 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32171

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->
When using `ReactDOM.unstable_createRoot()` with an invalid container it doesn’t throw a clear error. Instead, it leads to confusing issues like`Cannot call toLowerCase of undefined`.

React version:
React 19.0.0
## Steps To Reproduce

1. Call `ReactDOM.unstable_createRoot(<div>Hi</div>)` without a valid DOM container.
2. Try to use the returned root to render content.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->
Minimal code example
```
import ReactDOM from 'react-dom';

// Create a root with an invalid container
ReactDOM.unstable_createRoot(<div>Hello, world!</div>);

// Expectation: An error mentioning that the container is invalid.
```
## The current behavior
When an invalid container is passed to `createRoot()`, the function does not validate it. 
```
Cannot call toLowerCase of undefined
```
## The expected behavior
The createRoot() function should validate the container and show error.
```
unstable_createRoot(...): Target container is not a DOM element.
```


