# [React 19] useState's setter function becomes arity 2

> Issue #31578 - Created on 11/19/2024

> Original URL: https://github.com/facebook/react/issues/31578

## Description

## Summary

The setter from useState becomes arity 2 in React's 19.0.0-rc.1 release.

Haven't found a changelog entry (https://react.dev/blog/2024/04/25/react-19 or https://react.dev/blog/2024/04/25/react-19-upgrade-guide), neither looking at the commits, so I'm not sure if it's intentional or I might miss something here.

## Demo

React's 18 setStates is arity 1 https://codesandbox.io/p/sandbox/setstate-arity-1-react-18-pfdr3h
React's 19.0.0-rc.1 setState becomes arity 2 https://codesandbox.io/p/sandbox/setstate-arity-2-issue-react-19-x3l3kd
