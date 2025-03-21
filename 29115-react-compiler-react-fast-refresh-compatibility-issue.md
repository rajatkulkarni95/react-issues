# [React Compiler] React Fast Refresh Compatibility Issue

> Issue #29115 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29115

## Description

## Summary

When using the React Compiler, Fast Refresh is broken when importing a non-JavaScript file, .e.g.

```jsx
import content from "./content.md";

export const App = () => {
  return <div>{content}</div>;
};
```

In this example, if the content of the markdown file changes, then the app does not update without a page refresh. A repo for this example can be found at https://github.com/daniel-nagy/react-compiler-bug.

From a quick investigation, the issue appears to be that the compiler memo cache is global and that it does not treat imported values as _mutable_.
