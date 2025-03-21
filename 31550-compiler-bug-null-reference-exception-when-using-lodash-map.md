# [Compiler Bug]: null reference exception when using lodash map

> Issue #31550 - Created on 11/15/2024

> Original URL: https://github.com/facebook/react/issues/31550

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAKgmDgBTBEA2eFRAvgJRHAA6xRchjAHkQC8RADwATPADcAfJ25EiAfQB0AWwCGAB0r0KAGiKU2QmeyJdFVonjRG9OFbQSYA5jgAWRMwEY2862sYBBxYYlENGVEAekiAbktApkSgkLCxACMo6KyEhWYWRKYYyVk8xODQmGJ+PKYQJiA

### Repro steps

See the above playground. _.map can take null/undefined and just returns []. So the argument can be null.

Because the length is accessed inside the map callback, lodash ensures if the callback is called, the list is not null.

The compiler extracts the list.length outside the map, which then makes the code break.

Adding a un-necessary condition fixes the output.
https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAKgmDgBTBEA2eFRAvgJRHAA6xRchjAHkQC8RADwATPADcAfJ25E6DHEQBkqogH0AdAFsAhgAdK9CgBoilNkJnsiXRY6J40l0zm20EmAOY4AFkS2AIxs8k5OMAg4sMSi+jKiAPQJANwOEUwZkdGxYgBGiUmF6QrMLBlMyZKypRlRMTDE-KVMIExAA

### How often does this bug happen?

Every time

### What version of React are you using?

18.3.1

### What version of React Compiler are you using?

19.0.0-beta-a7bf2bd-20241110
