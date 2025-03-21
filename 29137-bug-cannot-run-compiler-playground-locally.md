# Bug: Cannot run compiler playground locally

> Issue #29137 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29137

## Description

After installing deps with `yarn` in the compiler workspace and building the babel plugin, next throws this error on running `yarn dev` in playground
```
Compiling /page ...
 ⨯ ./app/page.tsx
Error: Cannot find module '.../react/compiler/node_modules/babel-plugin-react-compiler/dist/index.js'. Please verify that the package.json has a valid "main" entry
```

https://github.com/facebook/react/pull/29122 should fix it but for some reason, it doesn't.

I was able to get it running locally by doing a yarn link on the babel plugin. Is this the intended way? Can we use the workspace to link the built plugin?

cc: @poteto 

