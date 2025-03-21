# Compiler String Concat Constant Propagation

> Issue #29617 - Created on 5/28/2024

> Original URL: https://github.com/facebook/react/issues/29617

## Description

Consider the following constant propagation:

Input:
```ts
function foo() {
  const a = "a" + "b";
  const c = "c";
  return a + c;
}
```
Output:
```ts
function foo() {
  return "abc";
}
```

Is this in scope for the react compiler? If so, is it open for contributions?
