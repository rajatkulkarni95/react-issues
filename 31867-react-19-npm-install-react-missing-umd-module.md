# [React 19] : npm  install react -- missing umd module

> Issue #31867 - Created on 12/20/2024

> Original URL: https://github.com/facebook/react/issues/31867

## Description

## UMD folder missing in React 19+ installation via npm

After installing React version 19.x.x using npm, the umd folder (which typically contains files like react.development.js and react.production.min.js) is missing from node_modules/react. These files are essential for UMD builds and are expected to be included in the package as per React's documentation. The same issue is observed for react-dom.

