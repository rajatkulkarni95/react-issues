# [Compiler Bug]: Invalid drop of memoization for string template literals

> Issue #29580 - Created on 5/24/2024

> Original URL: https://github.com/facebook/react/issues/29580

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEUYCAogB4AOCmYeAbggMo4x6YDmAFJ9VBzIiYdpy4BKIsAA6xIjAQ5YxUggCyCALYQePKQF4AfEQAGaCBAD0AEmAIadBswBilvpgE4JAX1MAaIgBtfkEAXQk5HzkQHyA

### Repro steps

If I call expensive function, for example some kind of hashing inside string literal React Compiler drops any memoization calling the expensiveFunction during every re-render.

```ts
function useExpensiveString(input) {
  return useMemo(() => `foo/${expensiveFunction(input)}`, [input])
}
```

gets compiled to 

```ts
function useExpensiveString(input) {
  let t0;
  t0 = `foo/${expensiveFunction(input)}`;
  return t0;
}
```

instead of 

```ts
function useExpensiveString(input) {
  const $ = _c(2);

  let t0;
  let t1;

  if ($[0] !== input) {
    t1 = `foo/${expensiveFunction(input)}`;
    $[0] = input;
    $[1] = t1;
  } else {
    t1 = $[1];
  }

  t0 = t1;
  return t0;
}
```

### How often does this bug happen?

Every time

### What version of React are you using?

current playground
