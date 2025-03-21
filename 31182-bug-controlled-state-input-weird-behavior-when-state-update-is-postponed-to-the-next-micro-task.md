# Bug: Controlled state input weird behavior when state update is postponed to the next micro task

> Issue #31182 - Created on 10/11/2024

> Original URL: https://github.com/facebook/react/issues/31182

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: v18.3

## Steps To Reproduce

1. Open the codesandbox link below
2. Add characters in the middle of each input
3. The first input works as expected. In the second input, the cursor will instantly jump to the end, also input methods will not work.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/74mhkd

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
By adding an additional queueMicrotask to the second input, two inputs behavior are different.


https://github.com/user-attachments/assets/5cc7e2f6-0706-43ef-88cd-08177ab59a35



## The expected behavior
Work loop stuff should not affect DOM manipulation.

Is it a bug or feature? Is it a react stuff?
