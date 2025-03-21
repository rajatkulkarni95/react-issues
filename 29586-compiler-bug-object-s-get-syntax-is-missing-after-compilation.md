# [Compiler Bug]: object's get syntax is missing after compilation.

> Issue #29586 - Created on 5/25/2024

> Original URL: https://github.com/facebook/react/issues/29586

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswBGWVwJ8AXhHj86-AHMEBQtABGlBADUylKAiGqJG-DB2w2AJnwAqfE4DcajQF8fvt50Pva4jvgAPIRMAG4AfMByCgB0elCGJmYWvhEA9NHxQf50IL5AA

### Repro steps

```ts
const state = {
  get doubleValue() {
    return 2 * 2;
  }
};
```

In the above code, doubleValue uses get syntax, and after compilation, it loses the `get` keyword and becomes an ordinary function. In this case the compiler should skip compilation until this syntax is supported.

I know that some syntaxes are currently unsupported by the react compiler, can we know what syntaxes are currently unsupported and in process?

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-4c2e457c7c-20240522
