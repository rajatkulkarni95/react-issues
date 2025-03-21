# [React 19] `transformOrigin` is Missing From Type `SVGAttributes`.

> Issue #29134 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29134

## Description

## Summary

In React 18 the following code worked with out error.

```jsx
<svg transform-origin="..." />
```

Since React 19, this will error. The required syntax is now

```jsx
<svg transformOrigin="..." />
```

However, `transformOrigin` is missing from `SVGAttributes`, so this results in a type error.

I was going to open a PR to add this but the types package for React 19 appears to be private.

## Workaround

```typescript
declare module "react" {
  interface SVGAttributes<T> {
    transformOrigin?: string | undefined;
  }
}
```
