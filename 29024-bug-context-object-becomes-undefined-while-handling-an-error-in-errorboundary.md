# Bug: Context object becomes undefined while handling an error in ErrorBoundary

> Issue #29024 - Created on 5/8/2024

> Original URL: https://github.com/facebook/react/issues/29024

## Description

React version: 18.2.0

## Steps To Reproduce

1. Clone https://github.com/vporton/react-undef-context
2. `yarn && npm start`
3. Click the button and watch console errors. (All of the sudden, a context object becomes `undefined`.)

Link to code example:

https://github.com/vporton/react-undef-context

## The current behavior
In browser console:
> Uncaught TypeError: Cannot set properties of undefined (setting 'hasError')

## The expected behavior
Should display the error `TEST EXCEPTION` in browser window in red font.
