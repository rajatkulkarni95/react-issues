# `react-compiler-healthcheck` prints "StrictMode usage not found." in Next.js project with `reactStrictMode: true` in `next.config.js`

> Issue #29130 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29130

## Description

## Summary

Can't provide a sandbox with Next.js I guess, but the case is rather simple. In Next.js, you don't manually add StrictMode, so the checks implemented in `compiler/packages/react-compiler-healthcheck/src/checks/strictMode.ts` won't apply. On top of these, we should add `reactStrictMode: true` detection in `next.config.js`, if the latter file is found.
