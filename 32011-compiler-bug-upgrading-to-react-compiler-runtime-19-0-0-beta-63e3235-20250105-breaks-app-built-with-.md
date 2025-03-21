# [Compiler Bug]: Upgrading to react compiler runtime 19.0.0-beta-63e3235-20250105 breaks app built with Vite + React Route v7

> Issue #32011 - Created on 1/8/2025

> Original URL: https://github.com/facebook/react/issues/32011

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/rishitells/react-router-v7-react-compiler

### Repro steps

React compiler setup breaks after upgrading the compiler related dependencies to 19.0.0-beta-63e3235-20250105.

Stack trace:
```
 [vite] Error when evaluating SSR module /app/root.tsx: failed to import "react-compiler-runtime"
|- /Users/rishabhsharma/Projects/react-router-v7/node_modules/.pnpm/react-compiler-runtime@19.0.0-beta-63e3235-20250105_react@19.0.0/node_modules/react-compiler-runtime/dist/index.js:17
import * as React from "react";
^^^^^^

SyntaxError: Cannot use import statement outside a module
    at wrapSafe (node:internal/modules/cjs/loader:1378:20)
    at Module._compile (node:internal/modules/cjs/loader:1428:41)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1548:10)
    at Module.load (node:internal/modules/cjs/loader:1288:32)
    at Function.Module._load (node:internal/modules/cjs/loader:1104:12)
    at cjsLoader (node:internal/modules/esm/translators:346:17)
    at ModuleWrap.<anonymous> (node:internal/modules/esm/translators:286:7)
    at ModuleJob.run (node:internal/modules/esm/module_job:234:25)
    at ModuleLoader.import (node:internal/modules/esm/loader:473:24)
    at nodeImport (file:///Users/rishabhsharma/Projects/react-router-v7/node_modules/.pnpm/vite@5.4.11_@types+node@20.17.12/node_modules/vite/dist/node/chunks/dep-CB_7IfJ-.js:53056:15)
    at ssrImport (file:///Users/rishabhsharma/Projects/react-router-v7/node_modules/.pnpm/vite@5.4.11_@types+node@20.17.12/node_modules/vite/dist/node/chunks/dep-CB_7IfJ-.js:52914:16)
    at eval (/Users/rishabhsharma/Projects/react-router-v7/app/root.tsx:5:31)
    at instantiateModule (file:///Users/rishabhsharma/Projects/react-router-v7/node_modules/.pnpm/vite@5.4.11_@types+node@20.17.12/node_modules/vite/dist/node/chunks/dep-CB_7IfJ-.js:52972:5)

```

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0

### What version of React Compiler are you using?

19.0.0-beta-63e3235-20250105
