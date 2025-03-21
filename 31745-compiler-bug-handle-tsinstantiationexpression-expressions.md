# [Compiler Bug]: Handle TSInstantiationExpression expressions

> Issue #31745 - Created on 12/12/2024

> Original URL: https://github.com/facebook/react/issues/31745

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhHCA7MAXABABwEMYwFcBeXAHgCUAaXAQQD4AKAN0IBsoFkmAlPxoVmuYAB0MuXAHpZBYqVwAzKBjjYAlplwB3LdgAWuSAFsyZwgHMtcXFqxaAJggB0HqTJgJssaZw8CFIAvlJSCAAe+BAweGoa2roAKgg4AMIQZvhaXAgwrALiXrjoWHjWvgAihNiEFLiForgACjBZWqRuPpBc7AisANoAugLh0nIAVLjJRp2lWTl5YKqOZJOyJWU4uM619ZSV2DV1hW7GCBisRCQIYxglstOz88bteiuE0vntMLgbjwU2zwezqDSOJ0IZwuVxupCoOBgjmsI2Y9xKPj8MGkVEYGAgFxgmWymEueECvHIwFBhBCcmYoSkIBCQA

### Repro steps

Basically, just use typescript's instantiation expressions inside a component

### How often does this bug happen?

Every time

### What version of React are you using?

19

### What version of React Compiler are you using?

19.0.0-beta-37ed2a7-20241206
