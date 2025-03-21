# Bug: React server components give type error in react 19

> Issue #28718 - Created on 4/2/2024

> Original URL: https://github.com/facebook/react/issues/28718

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
Canary (19.0.0-canary-95e6f032c-20240401)

## Steps To Reproduce

1. Create a react app with typescript
2. Make app.tsx a server component

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
https://github.com/InsightfulFuture/react-19-ts
<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
I get the error:
```
'App' cannot be used as a JSX component.
  Its type '() => Promise<JSX.Element>' is not a valid JSX element type.
    Type '() => Promise<JSX.Element>' is not assignable to type '(props: any, deprecatedLegacyContext?: any) => ReactNode'.
      Type 'Promise<Element>' is not assignable to type 'ReactNode'
```
when I make app an async component with use server

## The expected behavior
It works with app as a server component
