# Bug: unexpected `onClick` is triggered on button after pressing enter on another button

> Issue #30923 - Created on 9/9/2024

> Original URL: https://github.com/facebook/react/issues/30923

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

<img width="508" alt="image" src="https://github.com/user-attachments/assets/87025359-a74b-4f4e-baa4-d770f5308cad">

1. Use keyboard to navigate onto one of the `Press Enter on me` buttons
2. Press `Enter`

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://8wqvpr.csb.app/

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

On press `Enter`, you'll see an alert triggered by `onClick` from the button below

## The expected behavior

On press `Enter`, the button below should not be clicked, because the keydown event was triggered on the other button.

