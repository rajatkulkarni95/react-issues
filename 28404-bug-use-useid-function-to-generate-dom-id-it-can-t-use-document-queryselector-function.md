# Bug: Use useId function to generate dom id,it can't use document.querySelector function.

> Issue #28404 - Created on 2/21/2024

> Original URL: https://github.com/facebook/react/issues/28404

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:18.1.0

## Steps To Reproduce

1.```import {useId} from 'react' <div id={useId()}></div>```
2.```document.querySelector('#:r1:')```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:https://codesandbox.io/p/sandbox/hardcore-williams-yzyvqv

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Failed to execute 'querySelector' on 'Document': '#:r1:' is not a valid selector.

