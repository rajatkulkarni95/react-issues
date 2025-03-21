# Bug: Inconsistent enhanced error messages for incorrect hook calls

> Issue #32174 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32174

## Description

<!--
  PR #18480 included new error messages for invalid hook calls, but they don't always show up the way they should. The error message may not show up in some situations or may be ambiguous or inconsistent.
-->

React version: React 18.0.0 (also tested with React 19 beta)

## Steps To Reproduce

1.Use a React hook (like useState) outside of a custom hook or functional component.
2.Launch the program and look for error messages in the console.


Link to code example: https://codesandbox.io/s/new


## The current behavior
The message of error:

does not show up in certain situations.
appears, but offers no clear or practical advice on the matter.



## The expected behavior
The error message ought to:

When hooks are utilized improperly, they always show up.
Give precise, succinct, and doable instructions for fixing the problem.

