# [React 19] useOptimistic - Add option to disable rollback

> Issue #31595 - Created on 11/20/2024

> Original URL: https://github.com/facebook/react/issues/31595

## Description

## Summary

`useOptimistic` automatically rolls back upon error. Can we make this optional?

Use case: I would like to keep the optimistic data displaying upon error, and display a "Try again" button next to it. (yes, I could do this without useOptimistic, but I suspect this will be a common use case).

Also, the current rollback on error behavior [isn't documented here](https://react.dev/reference/react/useOptimistic), so suggest adding before release.

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

