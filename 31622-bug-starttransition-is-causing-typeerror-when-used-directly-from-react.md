# Bug: startTransition is causing TypeError when used directly from react

> Issue #31622 - Created on 11/23/2024

> Original URL: https://github.com/facebook/react/issues/31622

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

Getting this error message

`TypeError: Cannot read property 'add' of undefined`

1. Run the code example https://snack.expo.dev/@raajnadar/swr-error-in-expo-sdk-52
2. Run android or ios, the web version works without the error
3. Click the "Call the API button" button inside the mobile app
4. Check the logs tab, when switched to axios there is no issue
5. This happens with `swr` because it uses startTransition internally

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

Import like this

```
export const startTransition: (scope: TransitionFunction) => void =
  IS_REACT_LEGACY
    ? cb => {
        cb()
      }
    : React.startTransition
```
And use like this

```
startTransition(() =>
   setState({ data, isMutating: false, error: undefined })
)
```

Code from this repository https://github.com/vercel/swr/blob/1585a3e37d90ad0df8097b099db38f1afb43c95d/src/mutation/state.ts#L5-L10

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Getting this error when `startTransition` used from React directly

`TypeError: Cannot read property 'add' of undefined`

On Expo snack the error says

`Error: "Cannot read property 'add' of undefined" in TypeError: Cannot read property 'add' of undefined <<     at requestUpdateLane (/data/user/0/host.exp.exponent/files/.expo-internal/5cb1b0c52b8fcab94364327c83b808ee:18892:43) <<     at dispatchSetState (/data/user/0/host.exp.exponent/files/.expo-internal/5cb1b0c52b8fcab94364327c83b808ee:16726:33) <<     at anonymous (swr.mutation:12:14616)`

## The expected behavior

There is no TypeError,

When I tried using the `startTransition` from the `useTransition` hook the problem got solved
