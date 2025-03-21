# Bug: Rapid click fails to catch the onClick event properly

> Issue #28626 - Created on 3/25/2024

> Original URL: https://github.com/facebook/react/issues/28626

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. Open the address attached below in the mobile iOS environment
2. Touch the red and green boxes quickly and repeatedly

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://stackblitz-starters-3edcyj.stackblitz.io/

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

I think the issue reported here(#22521) is still happening. If you click the red and green boxes listed vertically and quickly, the green box's onClick event is ignored and the red onClick event is called twice. However, using the onTouchEnd event instead of the onClick event does not cause any problems.

As reported in the issue(#22521), the onClick event works normally in the vanilla js environment.
Thank you for taking a look :)

https://github.com/facebook/react/assets/26402298/29310705-66db-419a-91f8-0001a8132567

## The expected behavior

The onClick event of an element clicked by the user must be called correctly. Thank you!
