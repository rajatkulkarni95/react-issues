# Bug: useEffect misses run when running in StrictMode

> Issue #28304 - Created on 2/12/2024

> Original URL: https://github.com/facebook/react/issues/28304

## Description

React version: 18.2.0

## Steps To Reproduce

Link to code example: https://codesandbox.io/p/sandbox/quizzical-flower-tsd2xd?file=%2Fsrc%2FApp.js%3A22%2C1

Have a `useEffect` in strict mode. Make sure the variables in the dependency array changes on each render.


## The current behavior

Check the console log from the codesandbox. It will be something like this:

```
Dependency array outside of useEffect: 0,0
Dependency array outside of useEffect: 0,0
Dependency array inside of useEffect: 0,0
Dependency array outside of useEffect: 0,1
Dependency array outside of useEffect: 1,1
Dependency array inside of useEffect: 1,1
```

One would have expected a line like `Dependency array inside of useEffect: 0,1`.

## The expected behavior

When variables in the dependency array changes, `useEffect` should run with that specific scope.

## Questions

Is this an effect of something undocumented in strict mode? Could it happen outside of strict mode? The current documentation of `useEffect` does not specify if `useEffect` is guaranteed to run with the same scope that triggered the `useEffect`, but it sure feels like it should.
