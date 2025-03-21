# [Compiler Bug]: Compiler doesn't bail out when reading or writing `ref.current` during a render

> Issue #29161 - Created on 5/18/2024

> Original URL: https://github.com/facebook/react/issues/29161

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAegFQYDoDsAEG+AYlLnAC4CWEBAJhHAEYA2jA1snoft0diACaVBCzph8AQ3wwEAMwSzc1SSxYBPfGAqTWCfACV5+CEwBWCSvgoALSRXxUJqgO6T1YPvji0wTigjK+C5UttY2+gC2ENoyloEOAG6qUPoA5lSJgQB0Al5eAAowproaWjbQYrgA5A4+kQAOVCz6TJaSUGD6ofiRUDoBznFy+HSwVLhp4QheSnSK+MgAFPkERADKFVBi094Qjc0LcPZwNuFOAPx8aHhyZJQ0BJ0I6zp6RnJLySypAJT4wG4e1wsVkIwAvPhnh8vikEL8ANxAsHZOCwJQOSHfVJIghxCiwAhg3EAXzweEwODWJHu1Foo0YrA4XGp+RARgJMBBUmGigSVFUZQQAEcoKpvIKmJI4OwTAQEFkYJo5opcms2QBVXAsKjsfQAA2eAGFJdL2PqADS7Y5qKUyhkICS4CB1OyTfQuCK4LzzBqBebkEQSU6Sd25ECrHgAFRsTkcEmedEcBEioc0DRY0sdUjgxTAEmgMD28ylXWy+AAkhIemBJAovBQIFCutb9k0WkX6YXiwhS615BBZMEENUst4WqGEHQGxEW1AGlc1jdcHdyHSnl0TbazTCbSw7ex-oC8T4QQ4wfhIc9XqUELvTTLEeS8bJORuEFv92aVnj8PgltkgGSDAaRgP84IAHzDKi6IJABQEgWBFpAn+ADaKF-sMyG-vgAC62F-k+uAkiAJJAA

### Repro steps

Our codebase has a core hook called `useStableRef()` which breaks one of the rules of React by mutating a ref during render. This code doesn't trigger the `react-hooks` lint rules, nor does the new React compiler complain when encountering this code.

I'm putting this forth in the hopes that the React compiler will bail out when it encounters one of these hooks, instead of compiling these hooks and potentially breaking our codebase when we upgrade.

* `useStableRef` writes to `ref.current` in the hook's body. This is a side effect that occurs during rendering!
* `useCallbackRef` calls into `useStableRef` to return a non-reactive callback. In practice, we're using this as a poor-company's [`useEffectEvent()`](https://react.dev/learn/separating-events-from-effects), until that hook is stabilized. Should this function still compile if it calls a hook that doesn't compile?

### How often does this bug happen?

Every time

### What version of React are you using?

React Playground 2024-05-17
