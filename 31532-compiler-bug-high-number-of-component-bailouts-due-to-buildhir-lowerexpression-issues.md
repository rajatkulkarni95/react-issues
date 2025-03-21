# [Compiler Bug]: High number of component bailouts due to BuildHIR::lowerExpression issues

> Issue #31532 - Created on 11/13/2024

> Original URL: https://github.com/facebook/react/issues/31532

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [X] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

Private Repo. But it can be reproduced in any repo using the specific JS constructs

### Repro steps

1. Run React compiler healthcheck on the codebase.
2. Patch the healthcheck to log reasons/
3. Analyze the output logs.

The healthcheck revealed approximately 600 components are not compatible with the React compiler. The primary issues are related to BuildHIR::lowerExpression, with the following distribution:

Top issues by frequency:

1. Expected Identifier; got MemberExpression key in ObjectExpression (316 occurrences)
2. Handle tagged template with interpolations (260 occurrences)
3. Handle ThisExpression expressions (23 occurrences)
4. Expected Identifier; got TemplateLiteral key in ObjectExpression (20 occurrences)
5. Support ThrowStatement inside of try/catch (9 occurrences)

Additional notable issues:

1. Multiple expression types cannot be safely reordered (MemberExpression, BinaryExpression, CallExpression, ArrowFunctionExpression)
2. Issues with UpdateExpression handling within lambdas
3. Problems with computed properties in ObjectPattern

### How often does this bug happen?

Every time

### What version of React are you using?

18.2.0

### What version of React Compiler are you using?

19.0.0-beta-a7bf2bd-20241110
