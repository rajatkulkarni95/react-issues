# Bug: multiple useTransition hook in a page turn to activate first one

> Issue #31312 - Created on 10/21/2024

> Original URL: https://github.com/facebook/react/issues/31312

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.0.0

## Steps To Reproduce
As below codesandbox link
1. Click StartTransition2 button
2. see console show 'isPending true; isPending false'

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/usetransition-issue-68tfls?file=/src/App.js

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
1. Click StartTransition2 button
2. see console show 'isPending true; isPending false'


## The expected behavior
1. Click StartTransition2 button
2. see console show 'isPending2 true; isPending2 false'


## Note
Actually, I'm not really sure it's a bug or mine misunderstanding.
While hook is executed in function component by order (e.g. useState), each state hook memorize its own value, useTransition hook not do this in same way. I found it in another project, and simplify to codesandbox. The reason why I use two because I have two section in viewport relying on two sources (API) with different responding speed. I intend to let first response data show immediately and the other keep loading status by useTransition.


