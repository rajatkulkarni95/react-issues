# cannot upgrade `eslint` to v9 due to `eslint-plugin-react-hooks` peer dependancies

> Issue #30932 - Created on 9/10/2024

> Original URL: https://github.com/facebook/react/issues/30932

## Description

`eslint-plugin-react-hooks` does not currently support the latest version on `eslint`, `eslint@9.10.0`

React version: 18.3.1

## Steps To Reproduce

1. create a new react application
2. install `eslint` @ [8.56.0](https://www.npmjs.com/package/eslint/v/8.56.0)
3. install `eslint-plugin-react-hooks` @ [4.6.2](https://www.npmjs.com/package/eslint-plugin-react-hooks/v/4.6.2)
4. try to install `eslint` @ [9.10.0](https://www.npmjs.com/package/eslint/v/9.10.0)


Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
cannot install due to `eslint-plugin-react-hooks` only having `eslint` version 8 as a peer dependancy.

npm i output:

```bash
npm error code ERESOLVE
npm error ERESOLVE could not resolve
npm error
npm error While resolving: eslint-plugin-react-hooks@4.6.2
npm error Found: eslint@9.10.0
npm error node_modules/eslint
npm error   dev eslint@"^9.10.0" from the root project
npm error   peer eslint@"^7.5.0 || ^8.0.0 || ^9.0.0" from @babel/eslint-parser@7.25.1
npm error   node_modules/@babel/eslint-parser
npm error     dev @babel/eslint-parser@"^7.25.1" from the root project
npm error   6 more (@eslint-community/eslint-utils, ...)
npm error
npm error Could not resolve dependency:
npm error peer eslint@"^3.0.0 || ^4.0.0 || ^5.0.0 || ^6.0.0 || ^7.0.0 || ^8.0.0-0" from eslint-plugin-react-hooks@4.6.2
npm error node_modules/eslint-plugin-react-hooks
npm error   dev eslint-plugin-react-hooks@"^4.6.2" from the root project
npm error
npm error Conflicting peer dependency: eslint@8.57.0
npm error node_modules/eslint
npm error   peer eslint@"^3.0.0 || ^4.0.0 || ^5.0.0 || ^6.0.0 || ^7.0.0 || ^8.0.0-0" from eslint-plugin-react-hooks@4.6.2
npm error   node_modules/eslint-plugin-react-hooks
npm error     dev eslint-plugin-react-hooks@"^4.6.2" from the root project
npm error
npm error Fix the upstream dependency conflict, or retry
npm error this command with --force or --legacy-peer-deps
npm error to accept an incorrect (and potentially broken) dependency resolution.
npm error
```

## The expected behavior
ES lint is upgraded successfully

