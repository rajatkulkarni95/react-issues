# Bug: react-hooks/exhaustive-deps false positive

> Issue #31210 - Created on 10/14/2024

> Original URL: https://github.com/facebook/react/issues/31210

## Description

Linter seems to be incorrectly "complaining" about a missing dependency whenever calling a method from an object, the snippet below doesn't make sense by itself but trying to come with a minimal example in order to quickly explain the problem.

If I update to `result.refetch` instead of `result.refetch()` it would work, but that would obviously be completely different. The linter seems to properly interpret the dependency without raising any warning/error if not invoking the method

<img width="583" alt="image" src="https://github.com/user-attachments/assets/84940575-e86c-43ee-ae1c-db4d13a87e56">

React version: ^18

## The current behavior

React Hook useEffect has a missing dependency: 'result'. Either include it or remove the dependency array.eslint[react-hooks/exhaustive-deps](https://github.com/facebook/react/issues/14920)

## The expected behavior

There should be no warning as the dependency is passed in the dependencies array

