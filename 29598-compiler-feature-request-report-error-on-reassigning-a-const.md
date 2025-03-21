# compiler feature request: report error on reassigning a const

> Issue #29598 - Created on 5/27/2024

> Original URL: https://github.com/facebook/react/issues/29598

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAwhALYAOhCmOAFJTBJWAJRHAA6xRchYHEQDaADwA0RMAhwANALpEAvESjSAyjgCGOBPWBEAbloA2UBMiIByAIx2rRAL5sA3DyJ8BQwiQAWWzABzBGUiegQOJQA+TncPKRlZcIA6bRhgnGTjMwi3Xkc8jx9-IJCVekiYgwK4mBlYYno4jwAeKOb4lrxMSighbPMlYFEs03NHImKA4KGp0omAenbeeKIWvzwTABMiJY6Wvd5XHkcQRyA

### Repro steps

assign to constant variable will be transformed(maybe cause SSA?)
```js
  let onChange;
  let t1;

  if ($[1] === Symbol.for("react.memo_cache_sentinel")) {
    t1 = () => {};

    $[1] = t1;
  } else {
    t1 = $[1];
  }
  ```
  
  Expect to throw the error.

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-81c5ff2e04-20240521
