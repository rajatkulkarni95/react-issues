# [Compiler Bug]: if you use optional chaining, ref values can be read during render (new issue in the last few days)

> Issue #31272 - Created on 10/16/2024

> Original URL: https://github.com/facebook/react/issues/31272

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPASTsylwAKYPlYBlKACMAtkwIBfAJT5gAHTrr8+OKzAFpnAEql8AXnxQwCYyUGKA3Os34YCXLDYAeQkwBuL0lNgAxt5AD5nLU8uAGEIaWw6BDoCMgYACxwgkNIAfgA6OFhXFPl8AHoIti18T3KfXzDHOnkQeSA

### Repro steps

See the above playground. Remove the `?` optional chaining and you get an error.

good: 0.0.0-experimental-7c1344f-20241009
bad: 0.0.0-experimental-605e95c-20241015


### How often does this bug happen?

Every time

### What version of React are you using?

0.0.0-experimental-605e95c-20241015
