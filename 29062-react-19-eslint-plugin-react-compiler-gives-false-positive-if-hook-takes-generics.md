# [React 19]: `eslint-plugin-react-compiler` gives false positive if hook takes generics

> Issue #29062 - Created on 5/15/2024

> Original URL: https://github.com/facebook/react/issues/29062

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

(Not sure if this should be filed under React 19?)

The following code triggers `Hooks may not be referenced as normal values, they must be called. See https://react.dev/reference/rules/react-calls-components-and-hooks#never-pass-around-hooks-as-regular-values`

```ts
interface Data {}

function useHello() {
  const queryClient = useQueryClient();

  return useMutation<Data>({});
}
```

(`useQueryClient` and `useMutation` coming from `@tanstack/react-query`, fwiw)

Either removing the `<Data>` generic, _or_ the preceding `useQueryClient` resolves the error.

This is using `eslint-plugin-react-compiler@0.0.0-experimental-e04a001-20240515`

---

Anyways, I'm _super_ excited that you've finally open sourced this, and look forward to using it!

(I do wonder why `pretty-format@24` is used in the babel plugin tho 👀 very old!)
