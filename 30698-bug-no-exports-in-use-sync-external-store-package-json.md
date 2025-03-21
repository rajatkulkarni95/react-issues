# Bug: No "exports" in use-sync-external-store package.json

> Issue #30698 - Created on 8/15/2024

> Original URL: https://github.com/facebook/react/issues/30698

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 16.9

This is less of a critical error and more of suggestion to fix issue/non-ideal-scenario with certain webpack builds. I did not have permission to push a branch to this repo to make PR with.

## Steps To Reproduce

1. `import { useSyncExternalStore } from 'use-sync-external-store/shim';` in a library that uses `"type":"module"` in its package.json, and is then imported into an application built with webpack 5.
    - Be using webpack 5 _without_ setting `resolve: { fullySpecified: false }` in webpack config's module.rules[].resolve.
2. Receive an error:
     > BREAKING CHANGE: The request 'use-sync-external-store/shim' failed to resolve only because it was resolved as fully specified (probably because the origin is strict EcmaScript Module, e.g. a module with javascript mimetype, a "*.mjs" file, or a "*.js" file where the package contains '"type": "module"').

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

---

We have such an import line in our code. We also have an ESLint rule to prevent fully specified imports and do not want to make an exception. I would like to propose adding 'exports' to the [package.json in use-sync-external-store](https://github.com/facebook/react/blob/main/packages/use-sync-external-store/package.json) containing the following or similar:

```json
  "exports": {
    ".": {
      "default": "./index.js"
    },
    "./package.json": "./package.json",
    "./shim": {
      "default": "./shim/index.js"
    }
  }
```
(used [react's package.json](https://github.com/facebook/react/blob/main/packages/react/package.json#L24) as basis)

Have tested the above inside own project's node_modules/use-sync-external-store/package.json and confirmed this fixes the build error without needing to add in `resolve: { fullySpecified: false }` nor fully specify the path. Did not need package.json export, and did not need or test the "." export.


