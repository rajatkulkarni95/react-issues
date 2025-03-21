# Bug: dynamic import component  which use useMemo internaly failed

> Issue #27813 - Created on 12/8/2023

> Original URL: https://github.com/facebook/react/issues/27813

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. open https://codesandbox.io/s/import-memo-77vd7t?file=/App.js
2. the render page will show `Cannot read properties of undefined (reading 'length')`

![image](https://github.com/facebook/react/assets/49113249/9043a326-c323-4828-850d-47a72ff52f7b)


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
https://codesandbox.io/s/import-memo-77vd7t?file=/App.js
<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior


## The expected behavior

