# [Compiler Bug]: Compiler messes up with escape character

> Issue #32123 - Created on 1/19/2025

> Original URL: https://github.com/facebook/react/issues/32123

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswBVgGUoAIwC2TAgF58-BMPUA+EePzH8CAHSYYCAG4I6uACKkK1IQG4jJqXUiVzlCABzflEQBWVFNVwEQgBCUMEPCQBfJM8rXFg2EIljAB4SHGV8eSVVXHVgUpU1ZL1PE3w8pjpMKAJMMlxomDp1UNFRAHdQ-AB6etyTPMV23FZ8XE5MBH7wMrVQvQUa3Dyx2e7WScb9wphlE-xE8WTxEGSgA

### Repro steps

Steps:

1. Open playground link attached
2. Expect the input element in JS tab to be `<input pattern="\w" />`, but it is `<input pattern="\\w" />` instead, matching different regex than the one desired

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0

### What version of React Compiler are you using?

19.0.0-beta-63e3235-20250105
