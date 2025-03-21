# Bug: React 18 setState behaves differently when before and after Promise.resolve().then

> Issue #31669 - Created on 12/4/2024

> Original URL: https://github.com/facebook/react/issues/31669

## Description

The number of renders is different in React 18 when used before or after `Promise.resolve().then`. Here are the two examples:

````
  const handleClick = async () => {
    console.log(0);
    setV((v) => {
      console.log("y");
      return v + 1;
    });
    Promise.resolve().then(() => {
      console.log(1);
      setV((v) => {
        console.log("x");
        return v + 1;
      });
      console.log(2);
      Promise.resolve().then(() => {
        console.log(3);
      });
    });
    console.log(4);
    console.log(5);
  };

  const handleClick2 = async () => {
    console.log(0);
    Promise.resolve().then(() => {
      console.log(1);
      setV((v) => {
        console.log("x");
        return v + 1;
      });
      console.log(2);
      Promise.resolve().then(() => {
        console.log(3);
      });
    });
    console.log(4);
    setV((v) => {
      console.log("y");
      return v + 1;
    });
    console.log(5);
  };
```` 
 
`handleClick` causes two renders.
`handleClick2` causes one render.

React version: 18

## Steps To Reproduce

1. Go to this [link](https://codesandbox.io/p/sandbox/wr22w7?file=%2Fsrc%2FApp.js%3A7%2C1-48%2C1)
2. Click on **Welcome to CodeSandbox**

Link to code example:

1. Go to this [link](https://codesandbox.io/p/sandbox/wr22w7?file=%2Fsrc%2FApp.js%3A7%2C1-48%2C1)
2. Click on **Welcome to CodeSandbox**

## The current behavior

Both work differently.

## The expected behavior

Not sure. But not able to find any related documentation.
