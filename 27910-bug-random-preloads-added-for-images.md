# Bug: Random preloads added for images

> Issue #27910 - Created on 1/9/2024

> Original URL: https://github.com/facebook/react/issues/27910

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.0-canary-c29ca23af-20231205


## Steps To Reproduce

1. Render SSR app that has images in its tree using renderToString or renderToPipeableStream

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

![image](https://github.com/facebook/react/assets/305164/2cb278b5-bdd0-43e4-9252-6e054a9481c6)


## The expected behavior

To not insert preloads randomly.

Note that there is difference between renderToString and renderToPipeableStream, renderToString the preloads appear inside root and renderToPipeableStream they appear in head.

Sorry this is a bit of a question rather than bug report maybe, I have searched around and cannot see any mention of auto-preloading images but I assume there must be something going on that I have missed. 

I was able to fix by using `18.3.0-canary-493f72b0a-20230727`.



