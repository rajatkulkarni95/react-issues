# Bug: script element not suspending in canary

> Issue #28651 - Created on 3/27/2024

> Original URL: https://github.com/facebook/react/issues/28651

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: `18.3.0-canary-c3048aab4-20240326`

> If you supply an `src` and `async` prop, your component will suspend while the script is loading.
> \- https://react.dev/reference/react-dom/components/script#rendering-an-external-script

A slow loading script does not seem to cause React to suspend as expected from this description.

## Steps To Reproduce

1. Include a `<script src="…" async>` with a deliberate delay on the response
2. Observe that React canary does not suspend while the script is loading

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://replit.com/@DaveCardwell1/ConcernedGroundedDowngrade#index.js

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

This example contains a script where the server takes six seconds to respond. It changes the text `Slow script not loaded…` to `Slow script loaded!` once executed.

Note that it immediately displays `Script suspense done!`.

## The expected behavior

I expect it to display the `Suspended for script…` Suspense fallback message for six seconds before switching to `Script suspense done!` around the same time that the `Slow script loaded!` switch is made.
