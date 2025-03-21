# Bug: sample test

> Issue #32169 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32169

## Description

<!--

-->Currently, suspended nodes in React are hidden using display: none inline style. However, this is susceptible to being overridden by external styles. The new approach applies display: none !important, ensuring React's visibility style takes precedence and preserves the state of hidden components.

React version: 16.8.6

## Steps To Reproduce

1. Trigger a suspended state in a React component.
2. Apply an external stylesheet that includes a display: block !important rule targeting the component's DOM node.
3. Observe that external styles can override the inline display: none.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

External styles may override React’s style if !important is not applied.

## The expected behavior
React's display: none should remain effective regardless of external CSS.

