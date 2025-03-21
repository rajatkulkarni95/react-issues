# [React 19]: `eslint-plugin-react-compiler` defines no `main` in its package.json

> Issue #29068 - Created on 5/15/2024

> Original URL: https://github.com/facebook/react/issues/29068

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

`require('eslint-plugin-react-compiler')` fails - one has to do `require('eslint-plugin-react-compiler/dist/index.js')` instead. Happy to send a PR for this once you publish the source code.

Using `0.0.0-experimental-e04a001-20240515`
