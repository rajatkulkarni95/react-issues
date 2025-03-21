# [Compiler Bug]:  value read during render does not update when using `react-hook-form` `.watch` API

> Issue #29144 - Created on 5/18/2024

> Original URL: https://github.com/facebook/react/issues/29144

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/erikshestopal/react-compiler-bug

### Repro steps

**Reproduction steps:** 
1. Clone the repo
2. Run `bun install`
3. Run `bun dev` to start the dev server
4. Type in a value into the customer ID text field
5. Expect the address ID text field to show up but it does not

When trying to read a value during render using `react-hook-form`'s `.watch` API with the `babel-plugin-react-compiler` plugin enabled, the value is not updated and the component that is supposed to be rendered conditionally never renders. 

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-3f1436cca1-20240516
