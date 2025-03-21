# [React 19] `eslint-plugin-react-compiler` warning on destructured props mutation 

> Issue #29093 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29093

## Description

## Summary

Trying out `eslint-plugin-react-compiler`, it warns on the following code:

```tsx
function Foo({ ...props }) {
  props.foo = false;
  // Mutating component props or hook arguments is not allowed. Consider using a local variable instead
  return <div />;
}
```

Since `props` is destructured it's not mutating the original properties, so I believe this is a false positive.


