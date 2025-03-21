# [React 19] React warns about "fetchpriority" props

> Issue #28946 - Created on 4/29/2024

> Original URL: https://github.com/facebook/react/issues/28946

## Description

## Summary

In 18.2.0, React allowed the `fetchpriority` prop in all lower case, but did not accept camelized `fetchPriority`. Support for the camelized version was added in #25927, but it seems to have broken the lowercased version. This means there is no variant that works in both 18.2 and 18.3 canary/19 beta.

Repro: https://codesandbox.io/p/sandbox/nameless-bird-wvv84h

In 18.2.0 `fetchPriority` generates a warning but `fetchpriority` works without warning
In 18.3.0-canary and later, `fetchPriority` works but `fetchpriority` generates a warning. 
