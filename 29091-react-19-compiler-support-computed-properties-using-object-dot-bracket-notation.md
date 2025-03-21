# [React 19] Compiler: support computed properties using object dot/bracket notation

> Issue #29091 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29091

## Description

## Summary
Using `obj.value` or `obj['value']` in a computed property causes the compiler to not memoize the component.

Example:
https://playground.react.dev/#N4Igzg9grgTgxgUxALhAHQHYDMobgFwEsIMACAYQgFsAHEhDfACgEpThNTS4Sx9SIAIwBWpALztOXUgDcAhgBtkpAOQBrBAE8VAGikBfANxSeGPrMVQE4yWWkBtIcIB08hQF1l+GFb139UjAI+LBkADwAfGEA9BGYRpgg+kA

I see there is a todo prefix in the compiler error. Feel free to close if this is a known issue.
