# [Compiler Bug]: don't uses dependecies of useMemo

> Issue #29169 - Created on 5/19/2024

> Original URL: https://github.com/facebook/react/issues/29169

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhASwLYAcIwC4AEwUYCAsghhAL4EBmMEGBA5DAgIZx4sA6AdgIQAPHPnpR+3NBH4EyATwCCWLAApgBdvwAmCGAWoBKIgIEECcWWEL8OGBGAIBeAiXKUIatSecA+AgADJQAbPEYCABJgMg48AAsAOhgOXSYfakCAGgBtbT0YAF0jMzktBDxYOQAeAGEmLCUCOwcwZ2AWx2oAej8BalKhUVxCOklpWQJ67CUNZvsEQxNgUosrfhsJEJDOlyDoztoAJQgdGABbgHMoBAAvQNXyypganTQANz8ACQRtiAIAOq4EI6IhjbaHardN6fADc-RA1CAA

### Repro steps

1. Look at useMemo. 
2. Dependecies are not used in compilation

### How often does this bug happen?

Every time

### What version of React are you using?

playground
