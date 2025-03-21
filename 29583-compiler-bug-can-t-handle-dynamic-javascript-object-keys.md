# [Compiler Bug]: Can't handle Dynamic JavaScript Object Keys

> Issue #29583 - Created on 5/24/2024

> Original URL: https://github.com/facebook/react/issues/29583

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgdlAtgAgMoAuAhgVGDsADro75RyJhgBmUANgDTW0Cq6Y9Ri3ZcaOAEoIAVgjgEAlgDcEogL7VqCAB4AHCDAI5W6OfIg1CJMgBUiAcwAUOmBB1gAlBW4445sIeAcfytyVRwAXhxnVzANMV9+QwSCDENIqjFaAG1LUjAAOjxBBCZWNgBdZBwAHgBhCCw9dFSAQRwAegA+UVps3LJ8vgEGEuEKqrqGptSAIQ7u7z7iPPzJGVNlSpr6xvNU2vmenHV0bwT-HGI7QgBPNhKIr0ycHOWBopHS9i2AcgAjOwAWjsMAQGEBAEYAAxQnB-fQAEwQMDhiORwNB4IArDDLtoCBiwehAQB2GE-I5LEKDfjFL7jHD-IGghF4rQEgDuAAt5CkKYsXv0CmtZApNlUmYD9ER0HYEGzOTy+UcTt5QaQYDQHALqgilD42EQmAA5IhYBDhYBwNhgLQOH5XCmXey3e5gLLBPLldyqToC2hW8wpdAED1vMDlE69GrtPWKP1idzUVXoYymcw4HbTEMtByeDK0dWwGiUEAIiAldAOnBYEgpGClgDcyeoaYUGazexDMzzT0LCA1JbLFbAVcMtYI9abLdTUBM7ZoneaIdqvYLOCLmpwpfLlerE6nIGb6BOIFUQA

### Repro steps

```ts
enum Status {
  Successful,
  Unsuccessful,
  Rejective,
}

const content = {
  [Status.Successful]: <ComponentA />,
  [Status.Unsuccessful]: <ComponentB />,
  [Status.Rejective]: <ComponentC />,
}
```
When writing the above code within the component, it fails to compile.
It gets an error like this
> Todo: (BuildHIR::lowerExpression) Expected Identifier, got MemberExpression key in ObjectExpression (11:11)

### How often does this bug happen?

Every time

### What version of React are you using?

19
