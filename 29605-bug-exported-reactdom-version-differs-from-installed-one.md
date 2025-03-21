# Bug: Exported ReactDom.version differs from installed one

> Issue #29605 - Created on 5/28/2024

> Original URL: https://github.com/facebook/react/issues/29605

## Description

In react/react-dom 18.x versions, the exported version by the package differs from the one declared in `package.json`

React version: 18.x

## Steps To Reproduce

1. Check the minified `react.production.min.js` for version 18.0.0: https://unpkg.com/browse/react@18.0.0/cjs/react.production.min.js
```js
exports.version="18.0.0-fc46dba67-20220329"
```

Same happens for react-dom https://unpkg.com/browse/react-dom@18.0.0/cjs/react-dom.production.min.js

## The current behavior
The exported version does not match the installed version

## The expected behavior
The exported version is the same as the installed version
