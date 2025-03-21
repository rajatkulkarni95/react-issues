# Bug(react-hooks/exhaustive-deps): lint rule does not recognise typescript satisfies operator

> Issue #29766 - Created on 6/5/2024

> Original URL: https://github.com/facebook/react/issues/29766

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. Open https://stackblitz.com/edit/vitejs-vite-4arsvz?file=src%2FApp.tsx
2. On the terminal, run `npm run lint`.
3. There is not warning saying the `arr` reference changes. 
      If you remove the `satisfies` operator, you will get the warning back.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
https://stackblitz.com/edit/vitejs-vite-4arsvz?file=src%2FApp.tsx

## The current behavior
Eslint runs without warnings or errors.

## The expected behavior
Eslint should warn/error regardless of using `satisfies` operator
