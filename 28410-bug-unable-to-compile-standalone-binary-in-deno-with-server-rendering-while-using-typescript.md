# Bug: unable to compile standalone binary in Deno with server rendering, while using Typescript.

> Issue #28410 - Created on 2/21/2024

> Original URL: https://github.com/facebook/react/issues/28410

## Description

Hello! I am trying to build standalone binary with Deno, that renders static HTML to string with React. I am using `@react-dom/server` subpackage, but it seems that it doesn't works correctly in Deno if used in Typescript files.

React version: 18.2.0

## Steps To Reproduce

1. In Deno make a typescript file, and try to render something with SSR
2. Try to compile this file into standalone binary using `deno compile %filename%.ts`
3. Get an error

```bash
Check file:///workspaces/workspace/index.ts
error: Uncaught Error: Failed resolving package subpath './server' for '/deno-dir/npm/registry.npmjs.org/react-dom/18.2.0/package.json': [ERR_INVALID_PACKAGE_TARGET] Invalid "exports" target {"deno":"./server.browser.js","worker":"./server.browser.js","browser":"./server.browser.js","default":"./server.node.js"} defined for './server' in the package config /deno-dir/npm/registry.npmjs.org/react-dom/18.2.0/package.json imported from file:///workspaces/workspace/index.ts; target must start with "./"
    at Object.resolveModuleNames (ext:deno_tsc/99_main_compiler.js:687:28)
    at actualResolveModuleNamesWorker (ext:deno_tsc/00_typescript.js:119464:144)
    at resolveModuleNamesWorker (ext:deno_tsc/00_typescript.js:119856:22)
    at resolveModuleNamesReusingOldState (ext:deno_tsc/00_typescript.js:119951:16)
    at processImportedModules (ext:deno_tsc/00_typescript.js:121512:120)
    at findSourceFileWorker (ext:deno_tsc/00_typescript.js:121250:9)
    at findSourceFile (ext:deno_tsc/00_typescript.js:121115:22)
    at ext:deno_tsc/00_typescript.js:121064:24
    at getSourceFileFromReferenceWorker (ext:deno_tsc/00_typescript.js:121033:28)
    at processSourceFile (ext:deno_tsc/00_typescript.js:121062:7)
```

In JS files everything works fine.

Link to code example:

https://codesandbox.io/p/devbox/react-dom-server-deno-bug-svm3t7

## The current behavior

Build crashes if code from `@react-dom/server` is used.

## The expected behavior

Build completes successfully and binary works.

