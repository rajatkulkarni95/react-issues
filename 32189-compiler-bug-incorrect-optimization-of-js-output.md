# [Compiler Bug]:  Incorrect Optimization of JS Output

> Issue #32189 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32189

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

-

### Repro steps

1.Log in to the app.
2.Perform an action that triggers React Compiler optimization (e.g., render a specific component).
3.Observe that the output JS is incorrect, leading to broken functionality.

### How often does this bug happen?

Every time

### What version of React are you using?

18

### What version of React Compiler are you using?

18.0.0
