# Bug:  React component rendered with createPortal with state controlled by parents will not rerender on state change

> Issue #27926 - Created on 1/11/2024

> Original URL: https://github.com/facebook/react/issues/27926

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1.Download the project from https://stackblitz.com/edit/stackblitz-starters-qcvjsz
2. npm i && npm run dev

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://stackblitz.com/edit/stackblitz-starters-qcvjsz

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

My issue is explained on this live example : https://stackblitz.com/edit/stackblitz-starters-qcvjsz?file=src%2FApp.tsx

Basically I'm passing a list of options to a radio button list, with the state and setter to a child component rendered with createPortal, however when the options are clicked in the child the parent component updates it's state, but not the child, so the radio never showthe checked status.

## The expected behavior

The radios in the dialog show the checked status and different radio lists don't get updated at the same time

