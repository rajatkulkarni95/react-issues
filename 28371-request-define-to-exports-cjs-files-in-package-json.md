# Request: Define to exports cjs/* files in package.json

> Issue #28371 - Created on 2/18/2024

> Original URL: https://github.com/facebook/react/issues/28371

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0
I am encountering an issue when attempting to use React version 18.2.0 to build CJS to ESM support in browsers. The problem is related to the cjs folder not being defined in the "exports" field of the React package.json file.
Please check out this message error
https://github.com/esm-bundle/react/actions/runs/7909812813/job/21591452688?pr=303#step:6:16
```
[!] Error: Package subpath './cjs/react.development.js' is not defined by "exports" in /Users/vctqs1/Documents/developer/forked/react/node_modules/react/package.json
```
While `cjs` folder is not `exports`

## The current behavior

- `cjs` folder is not `exports`


## The expected behavior
-  `cjs` folder is able `exports` in package.json


