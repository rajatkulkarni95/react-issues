# Bug: Additional updater function call is not ignored in Strict Mode

> Issue #28700 - Created on 4/1/2024

> Original URL: https://github.com/facebook/react/issues/28700

## Description

When calling a setState with an updater function inside a useEffect, the additional call made in Strict Mode is not ignored, producing an unexpected state. The same behavior is NOT seen in React 17. From the docs:

> In Strict Mode, React will call your updater function twice in order to [help you find accidental impurities.](https://react.dev/reference/react/useState#my-initializer-or-updater-function-runs-twice) This is development-only behavior and does not affect production. If your updater function is pure (as it should be), this should not affect the behavior. **_The result from one of the calls will be ignored_**.

React version: 18

## Steps To Reproduce

1. Create a state that holds a number.
2. Include a call to its setState inside a useEffect, which adds +1 to the previous value.
3. Note that React will NOT ignore the additional call made in Strict Mode and will sum twice.

Link to code example: https://codesandbox.io/p/sandbox/zealous-thompson-htqfst?file=%2Fsrc%2FApp.js%3A16%2C1

## The current behavior
It is not ignoring the additional call to setState. In the example above, the result is 2.

## The expected behavior
It should ignore the additional call to setState. In the example above, the result should be 1.

