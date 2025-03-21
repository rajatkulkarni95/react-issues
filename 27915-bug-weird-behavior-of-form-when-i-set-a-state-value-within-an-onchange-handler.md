# Bug: Weird behavior of form when i set a state value within an onChange handler.

> Issue #27915 - Created on 1/10/2024

> Original URL: https://github.com/facebook/react/issues/27915

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. Wrap a form in a component (inside of the current component) and instantiate it on the jsx returned from the father component.
2. Bind the handler function to the form, within the onChange attr.
3. Create a state with the useState hook and set a new value when the onChange function handler is triggered.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: [code example](https://codesandbox.io/p/sandbox/modest-ully-zhw7xt?file=%2Fsrc%2FApp.tsx)

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

When i type anything or even interact with any input, the target dissipates and no value is stored in the input.
[Screencast from 2024-01-09 20-25-05.webm](https://github.com/facebook/react/assets/99749798/d4e439fb-aa1a-4fc6-a47a-2c5674c10bc4)

## The expected behavior

It should work as an usual form without re-rendering or dissipating the target.
