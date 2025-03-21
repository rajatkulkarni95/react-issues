# [React 19] ForwardRef props are not referentially stable, breaking downstream memoizations

> Issue #31613 - Created on 11/22/2024

> Original URL: https://github.com/facebook/react/issues/31613

## Description

## Summary

I don't know if this is a known behaviour or a bug, but something that's worth highlighting at least.

ForwardRef components are not deprecated, but they're not perfectly backwards compatible either.

The mere existance of `ref` prop on a ForwardRef component, even if `undefined`, makes the component `props` referentially unstable, breaking a whole host of downstream memoizations.

Reproduction:
https://codesandbox.io/p/sandbox/youthful-faraday-8m98cd?file=%2Fsrc%2FApp.tsx%3A34%2C23

React 18:
https://codesandbox.io/p/sandbox/youthful-faraday-forked-32lrwm?workspaceId=8a8eeabe-fead-479a-a993-25a9868e8015

If it's a known behaviour – please highlight this in the docs. Don't think we would have gone ahead with upgrading yet until some of our dependencies would be supporting React 19, because a whole host of packages (charting, datagrids, etc.) that are performance sensitive, suddenly had performance issues.

If not, it needs some attention, as it has pretty bad performance implications.

I believe a lot of maintainers are not dropping ForwardRef yet, because they think it's perfectly backwards compatible, and it's easier to maintain backwards compatibility for them.
