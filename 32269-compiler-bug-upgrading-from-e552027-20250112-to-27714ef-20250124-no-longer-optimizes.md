# [Compiler Bug]: Upgrading from `e552027-20250112` to `27714ef-20250124` no longer optimizes

> Issue #32269 - Created on 1/30/2025

> Original URL: https://github.com/facebook/react/issues/32269

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhHCA7MAXABAYQgFsAHZXAJQQEM5sA6AMX1wF5cAKASjYD5dgAHQy5c6LHgDaYBABsEdBABMAqjJhgANLhnYAynIXZlahBoC6bXFBl7s1YwB4YNJZlkBPXKZgB5GACCJACWPpLmvBzhXADcwsKi4jjW6gCSSmBWMvKKqupg9ETUJBwcNmY8rPzlMPTBSrHxImKYyXjs3HwCuAmiLRK41DAwVuFxGL2iAGYQIxxJeNlGJuq4EFMpZulgPELNfYPD9CQ2ABYcS7k+jfu4AL6TuC7YsBPND2+iz6+4GFCysnGd3GIDuQA

### Repro steps

No reproduction steps required - the playground shows the error.

https://github.com/facebook/react/pull/32093/files#diff-20b95f808e27819de316464ff5819940614b11b694deb9f1c4fecf39dff6b6e4R1607

As a workaround I've just extracted the function (in our real app it's a `queryFn` to `react-query`) outside of the component and pass it the arguments instead, so we no longer loop inside the component itself.

---

For future reference (for when this is fixed and the playground no longer shows an error), this is the current result:

<img width="670" alt="Image" src="https://github.com/user-attachments/assets/c9d632bb-f4b0-4ee4-8026-eb086cdbc3ea" />

### How often does this bug happen?

Every time

### What version of React are you using?

N/A

### What version of React Compiler are you using?

`27714ef-20250124`
