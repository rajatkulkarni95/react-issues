# Bug: eslint-plugin-react-hooks disallows the use of useId in async component even though it works

> Issue #31187 - Created on 10/11/2024

> Original URL: https://github.com/facebook/react/issues/31187

## Description

In #27045 the `eslint-plugin-react-hooks` has been modified to disallow the use of any hooks in `async` components, justified by this sentence:

> Hooks cannot be called in async functions, on either the client or the server. 

However, some hooks can be called in async components, namely `useId`. Or at least [the documentation](https://react.dev/reference/react/useId) does not mention it[^1].

[^1]: [The documentation for React 19](https://19.react.dev/reference/react/useId) does not mention it as well.

React version: 18.3.1
eslint-plugin-react-hooks: 5.0.0

## Steps To Reproduce

1. Create an async component that uses `useId`
```tsx
export default async function Component() {
  const id = useId();
  return null;
}
```
2. ESLint will throw the following error: 
```console
Error: React Hook "useId" cannot be called in an async function.  react-hooks/rules-of-hooks
```

## The current behavior

ESLint throws an error when an async component uses `useId`.

## The expected behavior

No ESLint error.
