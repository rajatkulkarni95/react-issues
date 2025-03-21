# Typo in dangerfile.js leads to unreachable code path

> Issue #32278 - Created on 1/31/2025

> Original URL: https://github.com/facebook/react/issues/32278

## Description

There is a typo in dangerfile.js which results in an unreachable code path which ought to be hit when there is no matching base artifact during DangerCI automated code review.

See: https://github.com/facebook/react/blob/221f3002caa2314cba0a62950da6fb92b453d1d0/dangerfile.js#L73
Compare: https://github.com/facebook/react/blob/221f3002caa2314cba0a62950da6fb92b453d1d0/dangerfile.js#L171
And the case which should hit this code path: https://github.com/facebook/react/blob/221f3002caa2314cba0a62950da6fb92b453d1d0/dangerfile.js#L160

Given the above context, the condition `Number === Infinity` is clearly meant to be `decimal === Infinity`, which it will be if the `catch` statement triggers when there is no matching base artifact. Without this fix, the primitive value `Infinity` is passed to `percentFormatter.format(decimal)`, resulting in the string `'+∞%'`. With this fix, the resulting string will be the intended `'New file'`.

## [PR 32277 resolves this](https://github.com/facebook/react/pull/32277)
