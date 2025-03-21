# [Compiler Bug]: Error Invalid hook call

> Issue #29202 - Created on 5/22/2024

> Original URL: https://github.com/facebook/react/issues/29202

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro
https://codesandbox.io/p/devbox/objective-spence-zrxvd7

### Repro steps

I am trying the new React 19 beta and the compiler throws an error when using the new `useActionState` hook and setting the `formAction` to the action of a form. When clicking a button, it throws this error:

![imagen](https://github.com/facebook/react/assets/107658697/855c9936-1c69-4693-b0bc-5ba5a5882f88)

Disabling the compiler, this works just fine.

If i create the function `changeInput` in the useActionState hook the error disappears

![imagen](https://github.com/facebook/react/assets/107658697/78e6d03f-f322-44ec-bf53-b52a6b6e2863)

![imagen](https://github.com/facebook/react/assets/107658697/0863d5eb-5ee9-4639-80fd-ec9b78ff8d5b)



### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-beta-26f2496093-20240514
