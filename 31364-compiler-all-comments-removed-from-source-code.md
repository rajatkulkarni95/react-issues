# [Compiler]: All comments removed from source code

> Issue #31364 - Created on 10/26/2024

> Original URL: https://github.com/facebook/react/issues/31364

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvhgJcsNgB4AfOPwr8cgMIQAtloR1cYblIBKCLRABuCQvgD0SiSo3bd+w1IAKUsAhhWb9spq9gDc4gC+4uK0DMys+Jo6egZGCKbm-kIiQXYAVPi4MGR0YJRkuDhgyPgApFX4UD4wdGS6AHT4ACoAFkxg+HAuyfgA7kyUlPgARgiSZpbW+Lm2QYMlBLgYBAC8+AD6e-wA5AASCBMQtWBHgmF0Qba2Xb39g0n6o+OTZJSQ07NSDLWNrKIJSGTNNSEJgWBTATboXDhOS2aGwu6Re50GKMFhsRKuFKeby+TLCMQSUQgRqzOiXXTmKl3FQPfKFYqlcqVap1ao05qtBAdHp9AZDD5jCb4OkEGZzIE2ZarVhgDZbfC7A7HM4XK43O45R7PUVvQmfKU-P5ygDWCEwuBBlIk4NkUJhcIRSJRaIUGJA4SAA

### Repro steps

I setup my Babel & webpack config to preserve comments, specifically comments for translators.

In systems like WordPress, i18n strings & comments are directly in the source code and must be preserved.

When React Compiler optimizes a component, all comments will be stripped.

When React Compiler is disabled, e.g. with `use no memo` or when it encounters a disabled lint rule, then the component won't be touched at all and comments are preserved as expected.

Unfortunately the Playground link doesn't show this, as it seems to strip all comments no matter what.

### How often does this bug happen?

Every time

### What version of React are you using?

17

### What version of React Compiler are you using?

0.0.0-experimental-34d04b6-20241024
