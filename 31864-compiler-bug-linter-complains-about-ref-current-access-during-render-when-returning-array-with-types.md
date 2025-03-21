# [Compiler Bug]: Linter complains about ref `current` access during render when returning array with Typescript's `as const`

> Issue #31864 - Created on 12/20/2024

> Original URL: https://github.com/facebook/react/issues/31864

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhASwLYAcIwC4AEwBUYCAwgIYA21ARpXANYA0JZASggGZukIBlPJTwICAXwLcYEDAQA6IGAkZ5FAbnkA7bQgAeOfFKha4eNBC3tBaAF4IAFAEoi2ggTiWwhANoATTAQtMAtgtjI8ABFA4NCwAF0CAF5rIRFHYDd3AgB3ND88AAtkAgAGFiz3QoQ0AHNCvBLyrPEnTR0rDy9CLGUANwtSAHk6Mhg+hBhk6y5uZ3asz2DCOFI8WVnp-ipaBmYHBy0IPwQXJIA+V073NG4CB16EAegwEbGJmAA6VZhlLTwXJlrtlHs9hqNJh9vrA-nhPgEwEstAgzPNKiD+oNXhDxpNob8goQUiYTtw0Mi-O1shJtOjbvcjicAPyfRkIAAqAE8sGIknyCAA5Y4IT4AUQAMqKALKigXsgD6AqGkVFgPR7iW3gIEBxH2myJyBC4IXsb0hkwOPkJME58TOlyB1Op9Ic1s5BAAZB6CG7PnRcCcYAAhCB6AR2U5XJ1OzWEYjk6jkmz2Ep5AqFNh0agQZjhlMEap1BoSZLq6M+-42v0ByYhsMRnyleILYHRiLRDBBEJeBzENNFNiF+qEVpU8viMuj2mt7W6vE696ONltMugrFm3FfH6w6YL80wMfuCedcRsHx2lvuZR4WBWHyrbwbHhsAKd2JeZvaY8gcRAA

### Repro steps

1. Copy the code above to a typescript file with react compiler linting.
2. Add `as const` to the end of the line returning `[customRef, dimensions]`.
3. The linter will suddenly complain about `Ref values (the `current` property) may not be accessed during render.`

### How often does this bug happen?

Every time

### What version of React are you using?

18.2.0

### What version of React Compiler are you using?

19.0.0-beta-201e55d-20241215
