# [Compiler Bug]: Make memoization more granular

> Issue #32424 - Created on 2/19/2025

> Original URL: https://github.com/facebook/react/issues/32424

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswBYPjAIy8ABb4AvvgC8+KAoDKilUPH5J02UTK4y6rToUARK2WN0TZujPwBbMnwSETtZ2hM74APyW1gB0vgJMuAjeWgB8+AlJwsj4ANoAuuLuUp40TNQIMAFBNtokZYkw1fxxmFXOADTyhnDKgoVuEpW4sGwAPABKCHTEjWGh1prAdeWVgc4aAPQp4mriIGpAA

### Repro steps

Example is provided in the [playground link](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswBYPjAIy8ABb4AvvgC8+KAoDKilUPH5J02UTK4y6rToUARK2WN0TZujPwBbMnwSETtZ2hM74APyW1gB0vgJMuAjeWgB8+AlJwsj4ANoAuuLuUp40TNQIMAFBNtokZYkw1fxxmFXOADTyhnDKgoVuEpW4sGwAPABKCHTEjWGh1prAdeWVgc4aAPQp4mriIGpAA)

In this example I would expect react compiler to memoize `mappedData` separately from the `filteredData` as I don't want to re-do the mapping each time when search string changes. 
What I would expect is for `filteredData` to have it's own memoization block with the `search` and `mappedData` as dependencies.


### How often does this bug happen?

Every time

### What version of React are you using?

19

### What version of React Compiler are you using?

latest
