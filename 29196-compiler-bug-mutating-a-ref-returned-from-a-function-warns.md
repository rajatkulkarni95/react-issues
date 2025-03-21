# [Compiler Bug]: Mutating a ref returned from a function warns

> Issue #29196 - Created on 5/21/2024

> Original URL: https://github.com/facebook/react/issues/29196

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEUYCAsgJ4BKCaAFAJRHAA6xRMCOsxpCtBowDc7AL7t2GbPkJEAEggA2SiExbsiROITA5OdIgF4SZKoKaiO-AKJo0CXPXVGAfBo5auaAHRxYXJj6JgDkOAh6IVZaYiLiIGJAA

### Repro steps

When consuming mutable refs from custom hooks (or via props), the consuming components should be allowed to mutate them inside effects/event handlers.

```js
function useMyRef() {
  return useRef('test');
}

function Hello() {
  const ref = useMyRef();
  useEffect(() => {
    ref.current = 'next';
//  ~~~ InvalidReact: Mutating a value returned from a function whose return value should not be mutated. Found mutation of `ref` (8:8)
  });
}
```

### How often does this bug happen?

Every time

### What version of React are you using?

19
