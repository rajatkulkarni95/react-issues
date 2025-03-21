# [Compiler Bug]:  babel-plugin-react-compiler@0.0.0-experimental-7779988-20241007

> Issue #31150 - Created on 10/8/2024

> Original URL: https://github.com/facebook/react/issues/31150

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://www.npmjs.com/package/babel-plugin-react-compiler

### Repro steps

[2024-10-08T04_56_44_562Z-debug-0.log](https://github.com/user-attachments/files/17288171/2024-10-08T04_56_44_562Z-debug-0.log)
[2024-10-08T04_56_44_562Z-debug-0.log](https://github.com/user-attachments/files/17288179/2024-10-08T04_56_44_562Z-debug-0.log)

Unable to create new expo project. Error when npm install in new project.

MAC Mini Apple M2, macOS 14.7

Fix:
Latest version  babel-plugin-react-compiler@0.0.0-experimental-7779988-20241007. contains problem. I replaced my old react expo project that works with 0.0.0-experimental-734b737-20241003

### How often does this bug happen?

Every time

### What version of React are you using?

react - 18.2.0, react-native - 0.74.5
