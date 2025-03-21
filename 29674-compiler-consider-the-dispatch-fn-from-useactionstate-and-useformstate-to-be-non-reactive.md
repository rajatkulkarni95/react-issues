# [Compiler]: Consider the `dispatch` fn from useActionState and useFormState to be non-reactive

> Issue #29674 - Created on 5/31/2024

> Original URL: https://github.com/facebook/react/issues/29674

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAwhALYAOhCmOAFAJRHAA6xRchYORA2gENcBTAGUcAnAgA0RACZ4wlSXAAWAQWGEAukQC8RKGASb8hcZIRMA3OyKduvPmggxyFqbIVKVqgGKu5LoGRggBbh5WjLaYdg6YPETmUABG5Hg4piL6REz6AHwscfbeyjhqWYQ2cQC+MXFcCbzJaRnh5Dl5eoVsHCWKZWrt1Rw17HEwCDiwxAA8ARBJYqnpmVqYesAtq5WYNUuiK22Bm9vHbvsA9PkxNSA1QA

### Repro steps

Align with #29665, considering the dispatch function returned by useActionState and useFormState to be non-reactive. 

This requires updating `REACT_APIS` in Globals.ts to define these hooks and their return type, and annotate the dispatch function as non-reactive. See the definition for `useState` as an example.

### How often does this bug happen?

Every time

### What version of React are you using?

19
