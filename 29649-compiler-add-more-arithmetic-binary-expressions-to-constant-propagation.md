# [compiler] Add more arithmetic binary expressions to constant propagation

> Issue #29649 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29649

## Description

There are already most arithmetic operators in constant propagation: `+`, `-`, `*`, `/`.
We could add more, namely: `|`, `&`, `^`, `<<`, `>>`, `>>>` and `%`:

Input:
```js
function f() {
  return [
    123.45 | 0,
    123.45 & 0,
    123.45 ^ 0,
    123 << 0,
    123 >> 0,
    123 >>> 0,
    123.45 | 1,
    123.45 & 1,
    123.45 ^ 1,
    123 << 1,
    123 >> 1,
    123 >>> 1,
    3 ** 2,
    3 ** 2.5,
    3.5 ** 2,
    2 ** 3 ** 0.5,
    4 % 2,
    4 % 2.5,
    4 % 3,
    4.5 % 2,
  ];
}
```
Output:
```js
function f() {
  return [
    123, 0, 123, 123, 123, 123, 123, 1, 122, 246, 61, 61, 9,
    15.588457268119896, 12.25, 3.3219970854839125, 0, 1.5, 1, 0.5,
  ];
}
```
