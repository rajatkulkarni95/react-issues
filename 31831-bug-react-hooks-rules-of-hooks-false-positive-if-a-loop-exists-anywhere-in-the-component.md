# Bug: [react-hooks/rules-of-hooks] False positive if a loop exists anywhere in the component

> Issue #31831 - Created on 12/18/2024

> Original URL: https://github.com/facebook/react/issues/31831

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

~React~ `eslint-plugin-react-hooks` version: 5.1.0

## Steps To Reproduce

1. Use a React hook (e.g. `useRef`) in a component function.
1. Also include a `for` loop in a component function, that the hook is not a part of.
2. The hook value will be flagged by the eslint rule, e.g.: "React Hook "useRef" may be executed more than once. Possibly because it is called in a loop. React Hooks must be called in the exact same order in every component."

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

```ts
export default function Test() {
  const myRef = useRef(1);

  for (let i = 0; i <= 5; i++) {
    console.log('test');
  }

  return myRef.current;
}
```


## The current behavior

The `useRef` call will be flagged by the rules-of-hooks plugin, since v5.1.0.

## The expected behavior

The `useRef` call will not be flagged, because it clearly is not called in a loop. This was the behavior as of v5.0.0.

