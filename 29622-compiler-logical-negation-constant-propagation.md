# Compiler Logical Negation Constant Propagation

> Issue #29622 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29622

## Description

Consider the following constant propagation:

Input:
```js
function foo() {
  const b = true;
  if (!b) {
    console.log("bar");
  } else {
    console.log("baz");
  }

  return {
    b0: !true,
    n0: !0,
    n1: !1,
    n2: !2,
    s0: !"",
    s1: !"a",
    s2: !"ab",
    n: !null,
  };
}
```

Output:
```js
function foo() {
  console.log("baz");
  return {
    b0: false,
    n0: true,
    n1: false,
    n2: false,
    s0: true,
    s1: false,
    s2: false,
    n: true,
  };
}
```

I think it can benefit dead code elimination. Is this in scope for the react compiler or is this considered as the job of the bundler? If so, is it open for contributions?
