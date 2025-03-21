# [Playground Bug]: Unexpected token, expected "{"

> Issue #31601 - Created on 11/21/2024

> Original URL: https://github.com/facebook/react/issues/31601

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)
- [x] Playground issue

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAejQAgPIAcEB2mcEBkANgpgIYEAmmUBJAti4QC4A6BGxpYDpgCiMGAEZMAXkwAKAJTSAfJgA8dAJYA3TGiUBuHnxJkhomACZpcxVJWz123UvmHeWE4JFiAzNcc6ejxGWAAqABYaYJgA7hAwANbRAGYaBAgh-KaYAMLWCsqYwJmYmDAIHLBEAc6ZAL4gdUA

### Repro steps

Any component created without curly braces will create an error in the console no compiler output is shown.

See playground link.

### How often does this bug happen?

Every time

### What version of React are you using?

react@rc

### What version of React Compiler are you using?

19.0.0-beta-8a03594-20241020
