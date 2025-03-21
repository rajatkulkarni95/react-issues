# No good alternative once this happens "Support for defaultProps will be removed from function components in a future major release"

> Issue #29233 - Created on 5/23/2024

> Original URL: https://github.com/facebook/react/issues/29233

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
18.3.1

Deprecation Warning:
> Support for defaultProps will be removed from function components in a future major release. Use JavaScript default parameters instead.

While the suggestion to use JS default params like `const Drawer = ({isOpen = true, showHandle = true}) => {}` seems like an excellent syntactic improvement, this _only_ works for the package maintainer.

Having the defaultProps as a static property enables configurability, where the application developer may be allowed to set the defaultProps for their own application, whereas javascript default parameters are set once by the package maintainer and never allowed to update.

This comes in to play most in the excellent recharts package, where props are passed to set the display of the charts. defaultProps are used to avoid these 3 props from being set on each instance of the `<Line/>` component.

``` javascript
Line.defaultProps = {
    ...Line.defaultProps,
    isAnimationActive: false,
    stroke: PRIMARY,
    strokeWidth: 2,
};
```

defaultProps saves hundreds of lines of code!

The alternatives are UGLY and I would not recommend them, I very much prefer the clean defaultProps way instead. In recharts what you have to do now is:

``` javascript
const myLine = (props) => (
    <Line strokeWidth={2} stroke={PRIMARY} isAnimationActive={false} {...props}/>
);
```

Ultimately the react team may have been too quick to dismiss defaultProps.
