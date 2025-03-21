# [Compiler Bug]: ref passed as prop cant be mutated in effects/events

> Issue #29741 - Created on 6/4/2024

> Original URL: https://github.com/facebook/react/issues/29741

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAwhALYAOhCmOAFMETAmkQL4CURwAOsUTiEwOIlEoATAIY4ERALxF63eQD5mrAHRxYLOgqIBGANz8iGnLGIAeAEJQcOQkUIkANnjgBrecHHTZdlU4D29rAHp7R0JVU0x2EHYgA

### Repro steps

```
function Component({ ref }) {
  const update = () => ref.current = 1;
  return <Button onClick={update}>click</Button>;
}

// InvalidReact: Mutating component props or hook arguments is not allowed. Consider using a local variable instead. Found mutation of `ref` (2:2)
```

### How often does this bug happen?

Every time

### What version of React are you using?

React 19
