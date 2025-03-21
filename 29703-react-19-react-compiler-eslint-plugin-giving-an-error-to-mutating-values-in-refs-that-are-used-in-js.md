# [React 19] React compiler & eslint plugin giving an error to mutating values in refs that are used in JSX

> Issue #29703 - Created on 6/1/2024

> Original URL: https://github.com/facebook/react/issues/29703

## Description

## Summary

`eslint-plugin-react-compiler` version: `0.0.0-experimental-51a85ea-20240601`

When I try to mutate a ref value in any event handler, the `eslint-plugin-react` compiler gives the following error:

```
ESLint: Updating a value used previously in JSX is not allowed. Consider moving the mutation before the JSX(react-compiler/react-compiler)
```

Linked CodeSandbox:

https://codesandbox.io/p/sandbox/kind-mirzakhani-qzw4t3

Linked Compiler Playground:

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwEFNMAKASn2AAdNvjiswNJpQQBJOpii4ASqXwBefFDAIVJADwAJACoBZADJyFuAKLSAtgjq4AfNzpVKvANzDh+UeIEABZkdITSMnbYeOr4fOrOAn7++EwkcSRSsvKKugB0cLAwjgQAhGoa7pSeSSIp+JkROcqkBUUleQBuZJRQCLGCIIM+dSmN2Vb5hTDFTgWUTHAA1nwj9QC+yesjycW4sGzcyf56zscpekzN+LgAnpgIakIg44Pr+MUkT+OWuaTvAHoznRzicAEaKXCsfCsADCC2WTxCYQiURwuHWzki0VwegBENwULowPqeJJ+G8wk2dBA6yAA

This seems a bit off to me because the documentation specifically mentions manipulating the DOM with a ref as an accepted pattern:
https://react.dev/reference/react/useRef#manipulating-the-dom-with-a-ref

@josephsavona made a [fix](https://github.com/facebook/react/pull/29591) for [issue](https://github.com/facebook/react/issues/29106) like this, but this fix allow only global mutations like `window` or `document`. Refs mutations also cause an error in eslint-plugin-react-compiler
