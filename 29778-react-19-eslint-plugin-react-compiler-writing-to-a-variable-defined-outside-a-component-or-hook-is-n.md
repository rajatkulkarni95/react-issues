# [React 19] eslint-plugin-react-compiler: “Writing to a variable defined outside a component or hook is not allowed. Consider using an effect”

> Issue #29778 - Created on 6/6/2024

> Original URL: https://github.com/facebook/react/issues/29778

## Description

## Summary

This is a stripped back example, but we have an event handler which updates some values on `document.cookie` for integration with a 3rd party library:

```
const handleOnAuthenticated = () => {
  document.cookie = `xyz`;
  setSomeState()
};
```

The linter warns us “Writing to a variable defined outside a component or hook is not allowed. Consider using an effect”. I wanted to check the advice was sound because I had been under the impression that doing things like this in a handler was preferred to useEffect.
