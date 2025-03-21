# [Compiler Bug]: eslint-plugin-react-compiler versioning strategy breaks semver

> Issue #31173 - Created on 10/10/2024

> Original URL: https://github.com/facebook/react/issues/31173

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Repro steps

semver sorts versions alpha-numerically but the version of each release is 0.0.0-experimental-HASH

So basically it is sorted by the hash... which makes renovate want to downgrade the compiler and ignore new versions.

Can you change it to

0.0.1-experimental-date-HASH

with the 0.0.1 from now on in order to break out from the current bad versioning strategy?


