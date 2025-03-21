# [React 19]: `react-compiler-runtime` always polyfills, even in React 19

> Issue #31482 - Created on 11/12/2024

> Original URL: https://github.com/facebook/react/issues/31482

## Description

## Summary

https://github.com/SimenB/react-19-compiler-runtime

Using `react-compiler-runtime` always loads the polyfill. Probably because `react` does not have the `__COMPILER_RUNTIME` export it's looking for.
