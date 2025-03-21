# [React 19] Discard ongoing action?

> Issue #31734 - Created on 12/12/2024

> Original URL: https://github.com/facebook/react/issues/31734

## Description

## Summary

I tried to implement _search as you type_ component (see: https://codesandbox.io/p/devbox/k3dvwn) and found that the `useActionState` + `startTransition` doesn't discard outdated requests, e.g. if I type `apple`, `useActionState` will wait for the ongoing request to finish, before starting next one, to get results of the `ap` react waits for `a` to resolve.

Is it an expected behavior? How can I discard ongoing request?


https://github.com/user-attachments/assets/f0b6f508-a97e-4feb-b50d-ee95736e03fb




<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

