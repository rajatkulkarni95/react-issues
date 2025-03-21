# Bug: Hydration error due to <button> 

> Issue #28545 - Created on 3/12/2024

> Original URL: https://github.com/facebook/react/issues/28545

## Description



<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:

## is there any way to fix this issue
Unhandled Runtime Error
Error: Hydration failed because the initial UI does not match what was rendered on the server.
See more info here: https://nextjs.org/docs/messages/react-hydration-error

In HTML, <button> cannot be a descendant of <button>.
This will cause a hydration error.



                              <button>
                              ^^^^^^^^
                                <_c>
                                  <button>
                                  ^^^^^^^^

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

https://github.com/JAGADEESHWARAN20/Shopwithdashboard/blob/main/app/(dashboard)/%5BstoreId%5D/(routes)/settings/components/SettingsForm.tsx

