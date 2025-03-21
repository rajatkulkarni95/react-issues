# Bug: Property 'inputType' does not exist on type 'Event'

> Issue #28517 - Created on 3/7/2024

> Original URL: https://github.com/facebook/react/issues/28517

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.0.0

## Steps To Reproduce
<img width="458" alt="image" src="https://github.com/facebook/react/assets/52973358/5beea44e-13b6-4653-8b0d-88496e63bd82">

create an `onChange` handler for an `input` and try to access `event.nativeEvent.inputType`

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
https://playcode.io/1790904

## The current behavior
Doesn't allow type


## The expected behavior
Should allow property access
