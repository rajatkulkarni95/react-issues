# Bug: Props with `propTypes` treated as required in TypeScript [React 19]

> Issue #31952 - Created on 1/2/2025

> Original URL: https://github.com/facebook/react/issues/31952

## Description

React version: 19.0.0

## Steps To Reproduce
After upgrading React to version 19, we noticed that properties in legacy components written in .jsx using propTypes are being treated as required when used in .ts files, even if they are not explicitly marked as isRequired.

***EDIT***
It seems that `propTypes` are being ignored, but the type is somehow interfered and is build based on the function arguments definition inside `jsx` file.
```
{ children: any; style: any; isLoading: any; shadow: any; qaId: any; className: any; }
```

Is there any possibility to disable it?

Here’s an example component:

```.jsx
export const PageBox = ({ children, style, isLoading, shadow, qaId, className }) => ({ ... });

PageBox.propTypes = {
  qaId: PropTypes.string,
  children: PropTypes.node,
  style: PropTypes.object,
  isLoading: PropTypes.bool,
  shadow: PropTypes.oneOf(["none", "regular"]),
  className: PropTypes.string
};
```

When trying to use this component, TypeScript throws the following error:

```
Type '{ children: Element[]; className: string; }' is missing the following properties from type '{ children: any; style: any; isLoading: any; shadow: any; qaId: any; className: any; }': style, isLoading, shadow, qaIdts(2739)
```

## The current behavior
All props are being treated as required, even when they are not marked as isRequired in the propTypes definition.

## The expected behavior
Only props explicitly marked as isRequired should throw a TypeScript error.
