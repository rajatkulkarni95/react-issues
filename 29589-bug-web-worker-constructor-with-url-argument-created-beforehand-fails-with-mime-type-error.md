# Bug: Web worker constructor with URL argument created beforehand fails with MIME type error

> Issue #29589 - Created on 5/25/2024

> Original URL: https://github.com/facebook/react/issues/29589

## Description

When working with React and Web Workers I noticed strange bug that is visible when the new worker URL arguments is not created directly within web worker's constructor. 

````ts
// this works just fine ✅ 
const worker = new Worker(new URL("worker.ts", import.meta.url)); 

// but this fails ❗ 
const path = new URL("worker.ts",import.meta.url);
const worker = new Worker(path); 

// error:
// Refused to execute script from '<URL>' because its MIME type ('video/mp2t') is not executable.
   
// interestingly this will work too (but the worker need to switched to JavaScript) ✅ 
const path = new URL("worker.js", import.meta.url);
const worker = new Worker(path);
````

React version: 18.3.1

## Steps To Reproduce

1. Create new worker file in React + TypeScript project (eg. 'worker.ts')
2. Create a URL object: `const path = new URL("worker.ts",import.meta.url);`
3. Try to create a Worker object `const worker = new Worker(path);`
4. run `npm run start` (mine use `react-scripts start`)

Pictures:
The issue while rendering the scene:
![image](https://github.com/facebook/react/assets/1651451/cfa73d28-8a6e-4d27-ae7c-d27e2daa1b8d)

The rendering scene code:
![image](https://github.com/facebook/react/assets/1651451/6e053327-85ed-4f51-88b0-c541c0743504)



## The current behavior
Throwing a MIME type error

## The expected behavior
Compile succesfully and run worker without issues
