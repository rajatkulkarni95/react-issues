# [React 19] RSC and `as` property pattern

> Issue #30706 - Created on 8/15/2024

> Original URL: https://github.com/facebook/react/issues/30706

## Description

## Summary

Many UI libraries adopt the `as` property pattern, especially for the Icon component.

```
<Icon as={ArrowIcon} />
```

This pattern is currently unsupported by server components, and requires to manually define client components for each icon one decides to use.

Is there a suggested alternative pattern the React team would like to promote? If not, do you think passing components as properties could be supported? In theory a component could be serialized (to a pointer) and then sent over HTTP, then the client could either dynamically import it, or the bundler could statically analyze it and bundle it on the client side code.

Alternatively, when a component is passed as property, the server component could inline the child component so that they are forced to be render together.
