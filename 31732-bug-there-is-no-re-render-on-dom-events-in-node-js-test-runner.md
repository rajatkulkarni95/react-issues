# Bug: There is no re-render on DOM events in Node.js test runner

> Issue #31732 - Created on 12/11/2024

> Original URL: https://github.com/facebook/react/issues/31732

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

Hi, I tried to write tests with Node.js test runner with `jsdom` but this is not working.

Initial render and mount works fine.

But when event is dispatched (click for example) there is no re-render of component.

React version: 18.3.1

#### Guides I used

- https://nodejs.org/en/learn/test-runner/using-test-runner

## Steps To Reproduce

0. Have Node.js 20+ 
1. Clone repository https://github.com/krutoo/node-test-runner-react-dom
2. `npm i`
3. `npm run test`

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://github.com/krutoo/node-test-runner-react-dom

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

There is no re-render of component after event is dispatched and as result test is failed

## The expected behavior

Test is done successfully 
