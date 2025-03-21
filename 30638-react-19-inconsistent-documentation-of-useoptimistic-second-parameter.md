# [React 19] Inconsistent documentation of useOptimistic second parameter

> Issue #30638 - Created on 8/8/2024

> Original URL: https://github.com/facebook/react/issues/30638

## Description

## Summary
[Main docs](https://react.dev/reference/react/useOptimistic) show that useOptimistic has a required second parameter updateFn.

[The RC blog post](https://react.dev/blog/2024/04/25/react-19#new-hook-optimistic-updates) does not, though.

The current version, [19.0.0-rc-e948a5ac-20240807](https://www.npmjs.com/package/react/v/19.0.0-rc-e948a5ac-20240807), seems to work without the second parameter ([example](https://codesandbox.io/p/sandbox/use-optimistic-multiple-n6hr29?file=%2Fsrc%2FApp.js)).

I opened the ticket here and not in the documentation repo, because this is about the upcoming version, and it seems there might not be clarity on what should be the expected behavior. Forgive me if it still was supposed to go on the other repo.
