# Bug: Despite having implemented optimizations such as shouldComponentUpdate or PureComponent

> Issue #28406 - Created on 2/21/2024

> Original URL: https://github.com/facebook/react/issues/28406

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:

## Steps To Reproduce

am currently working on a complex React project, which uses several components with a large number of children. However, I have noticed that the performance of the app has been significantly impacted by the rendering of these components.

Despite having implemented optimizations such as shouldComponentUpdate or PureComponent, the performance is still far below what I would expect. Even scrolling becomes slow and laggy.

I was wondering if there are any best practices or recommendations for optimizing the rendering of complex components in React? Are there any common mistakes that I might be making that could be causing these performance issues?

Any advice or suggestions would be greatly appreciated.

Thanks in advance!

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


## The expected behavior

