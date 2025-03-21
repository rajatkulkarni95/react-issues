# Bug: Found an error on React Documentation Site

> Issue #27986 - Created on 1/18/2024

> Original URL: https://github.com/facebook/react/issues/27986

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: Official Documentation site (`https://react.dev/learn/state-a-components-memory`)

## Steps To Reproduce

1. Go to `https://react.dev/learn/state-a-components-memory`
2. On right side menu section -> Click on **Adding a state variable** 
3. 3. see the image ->  ![image](https://github.com/facebook/react/assets/122859066/0217f9f4-9166-4796-8186-c58aec1911bd)
4. Go to the last by clicking on the Next button, and click on the Next button again.
5. You will see the error -> ![image](https://github.com/facebook/react/assets/76896592/e49b7b4d-1645-4134-80f8-94cedf01e986)


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
next button not disabled or handle the error

## The expected behavior
Need to Disable the Next button and then handle the issue, but also generate the previous button for go back.
