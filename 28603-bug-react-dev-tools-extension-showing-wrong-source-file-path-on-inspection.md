# Bug: React Dev tools extension showing wrong source file path on inspection

> Issue #28603 - Created on 3/21/2024

> Original URL: https://github.com/facebook/react/issues/28603

## Description

When we try to inspect the component using react-dev-tools to find the file's path and line number, it is now showing path to file from some build folder (like *.mjs, *.js) rather than from the actual source file, I think something happened recently which somehow break down this very useful functionality.


![issue_react_devtools](https://github.com/facebook/react/assets/47815255/254320f5-37f2-4e8a-bc27-5ade377d143b)


React version:

## Steps To Reproduce

1. Run any react application in development mode
2. try to inspect the component from react-dev-tools and check its source

you can also clone this respository: https://github.com/gittyvarshney/phoneBook
`git clone https://github.com/gittyvarshney/phoneBook.git`
`npm install `
`npm run dev`
