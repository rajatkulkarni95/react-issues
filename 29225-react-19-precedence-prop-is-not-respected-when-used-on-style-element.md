# [React 19] precedence prop is not respected when used on style element

> Issue #29225 - Created on 5/23/2024

> Original URL: https://github.com/facebook/react/issues/29225

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

Setting the `precedence` prop on a `style` element with a unique `href` does not seem to have any affect and the style elements will be ordered based on where they were in the React tree. 

[CodeSandbox Demo](https://codesandbox.io/p/sandbox/react-style-precedence-bug-yxfs24?file=%2Fsrc%2FApp.js%3A9%2C15)

I expected the style tags to be grouped and ordered based on precedence. [This PR](https://github.com/souporserious/restyle/pull/3) shows an example of the output when used with an atomic class name approach.

