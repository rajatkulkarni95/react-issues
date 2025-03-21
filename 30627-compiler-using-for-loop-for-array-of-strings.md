# [Compiler]: Using `for` loop for array of strings

> Issue #30627 - Created on 8/7/2024

> Original URL: https://github.com/facebook/react/issues/30627

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/facebook/react/blob/9eb288e6579333612ed736c4e088669daf90a076/compiler/packages/babel-plugin-react-compiler/src/Entrypoint/Program.ts#L266

### Repro steps

Hello @gsathya ,

I was wondering if the `for ... in` was intended instead of `for ... of`.

I think `for ... of` is more recommended for array of strings (`Array<string>`) like in this case. 

Thanks!

### How often does this bug happen?

Every time

### What version of React are you using?

18.3.1
