# Bug: errors caught by error boundaries appear in console twice

> Issue #28385 - Created on 2/20/2024

> Original URL: https://github.com/facebook/react/issues/28385

## Description

When an error boundary catches an error, the error appears _twice_ in the console, which used to be _once_ in older React versions.

Additional observations:
- `componentDidCatch` only fires once, as expected.
- After catching the error, the error boundary gets remounted with its _initial_ state (`{ hasError: false }` in the linked example) — this is not expected.

React version: 18.1.0.

## Steps To Reproduce

Link to code example: 
https://codepen.io/grebenyuksv/pen/vYPvvvY?editors=1111.

This appears in the console _twice_:
```
Uncaught Error: Very unexpected error
    at TestComponent ...
```

## The current behavior
The error appears _twice_ in the console.

## The expected behavior
The error should only appear _once_ in the console — at least, it used to be so in older React versions.
