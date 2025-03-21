# Bug: useFormState formAction becomes null in strict mode

> Issue #28556 - Created on 3/14/2024

> Original URL: https://github.com/facebook/react/issues/28556

## Description

The form action returned from the hook `useFormState` becomes null when using React strict mode. It causes the page to reload on the submission of the form and the action does not work. I know that the React strict mode performs some actions twice intentionally to find unexpected behavior in the development. But, it would be better if we could use it without disabling the Strict mode.

React version: 0.0.0-experimental-bb0944fe5-20240313

## Steps To Reproduce

1. Enable strict mode
2. Submit the form that uses form action returned from useFormState

Link to code example:
https://codesandbox.io/p/sandbox/jolly-minsky-kmkspd
https://codesandbox.io/p/sandbox/damp-tree-yv2vzy

## The current behavior
Form action becomes null causing the page to reload.

## The expected behavior
Form action should be a function provided as the argument in the `useFormState` hook.
