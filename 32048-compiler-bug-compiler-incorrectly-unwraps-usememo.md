# [Compiler Bug]: Compiler incorrectly unwraps `useMemo()`

> Issue #32048 - Created on 1/12/2025

> Original URL: https://github.com/facebook/react/issues/32048

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAkjggLYAUADjBDWAJRHAA6xRchYOrX0THwC+RALxE6DMAG4OHIgMy8iAE3FEoYBAFlKEKlRZiAfKwWKlKzBADuGmghhoIMCgENsCAHQ3bRuU5FbmUIABsfMIgAcyo2EBIiaIQ+GAQ4dzC4KDD3clUAQnimQItFWwALPAiiWicXN09EXzsjIgBaIj8iAB4iADYWYGF5IKI0nFhibiwcb1VAxWEAGiIAbRmheYBdEtHFCanast7VPAA3ExPFYAApAGUAeQA5b14YPExovDQATypNjgmCtWA8Xm8cB8vj9-qpgScegB6M6XCx7TAjTAgYRAA

### Repro steps

In the original code, the useMemo internals (the artificial pause) are executed only when `count.d` changes. However, the compiler unwraps the code incorrectly, causing it to execute regardless of the value of `count.d`.

### How often does this bug happen?

Every time

### What version of React are you using?

latest

### What version of React Compiler are you using?

latest
