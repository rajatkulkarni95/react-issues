# [Compiler Todo]: (BuildHIR::lowerExpression) Handle `MetaProperty` expressions

> Issue #29737 - Created on 6/3/2024

> Original URL: https://github.com/facebook/react/issues/29737

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAhgBQCURwAOsUTAjrMXgLYAOEMOAdG0xK8EmAG4BuOgF8QUoA

### Repro steps

I'm using [compile-time env vars using Vite](https://vitejs.dev/guide/env-and-mode#env-files). It works by accessing `import.meta.env.VITE_VAR_NAME`. The react compiler does not seem to handle these expressions:
```js
function a() {
  return import.meta.env;
}
```

Since react-compiler cannot know to what value _anything_ on the `import.meta` object resolves, it should just be passed down, resulting in the same code.

Note:
I tried to implement support for it, but I'm not able to test it aside from running it in the playground:
https://github.com/facebook/react/compare/main...nikeee:react:meta-property?expand=1

The test runner does not support anything related to `import`, since the code must be executed as a module, which is not possible in `eval`.


### How often does this bug happen?

Every time

### What version of React are you using?

19
