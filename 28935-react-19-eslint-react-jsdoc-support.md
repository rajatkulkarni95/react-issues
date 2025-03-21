# [React 19] Eslint React JSDoc support

> Issue #28935 - Created on 4/27/2024

> Original URL: https://github.com/facebook/react/issues/28935

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

based on react 19 documentation `prop-types` is gone, so for JS users the only way to manage it is using JSDoc, can be possible to support jsdoc prop-type validation in eslint-plugin-react ?

Example
```js
/**
 * @param {{
 *   content?: string,
 *   requiredParameter: string // required parameter if not can be with "?"
 * }} props
 * @returns {React.ReactElement}
 */
const ChildElement = props => {
  const { content = '' } = props;

  return <div>{content}</div>;
};

/** @returns {React.ReactElement} */
const ParentElement = () => {
  return <ChildElement content="Hello World" wrongParameter="test" />;
};
```

in this example
* wrongParameter should be marked as error due that is not in ChildElement JSDocs
* whole component should mark an error due that requiredParameter that exists in the JSDoc is not defined from the parent element

the intention of this request if to give some ways in javascrit to work without involve typescript to maange types and props
