# Bug: Cannot create new react app

> Issue #31934 - Created on 12/30/2024

> Original URL: https://github.com/facebook/react/issues/31934

## Description

```bash
> npx create-react-app loldinardelay

npm error code ERESOLVE
npm error ERESOLVE unable to resolve dependency tree
npm error
npm error While resolving: loldinardelay@0.1.0
npm error Found: react@19.0.0
npm error node_modules/react
npm error   react@"^19.0.0" from the root project
npm error
npm error Could not resolve dependency:
npm error peer react@"^18.0.0" from @testing-library/react@13.4.0
npm error node_modules/@testing-library/react
npm error   @testing-library/react@"^13.0.0" from the root project
npm error
npm error Fix the upstream dependency conflict, or retry
npm error this command with --force or --legacy-peer-deps
npm error to accept an incorrect (and potentially broken) dependency resolution.
npm error
npm error
npm error For a full report see:
npm error C:\Users\monik\AppData\Local\npm-cache\_logs\2024-12-30T08_15_02_751Z-eresolve-report.txt
npm error A complete log of this run can be found in: C:\Users\monik\AppData\Local\npm-cache\_logs\2024-12-30T08_15_02_751Z-debug-0.log
```
