# [Compiler Bug]: Incorrect Handling of onLoad and onError Events in <link> Component

> Issue #32166 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32166

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

-

### Repro steps

1.Render a <link> element with rel="preload", onLoad, and onError attributes.
2.Simulate onLoad and onError events in the environment.
3.Observe that the events are not handled as expected by the compiler.


### How often does this bug happen?

Every time

### What version of React are you using?

16.0.0

### What version of React Compiler are you using?

Latest version
