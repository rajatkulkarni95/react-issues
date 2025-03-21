# The const array variable value populated in a function does not reflect the updated values when called in another function in Firefox

> Issue #29947 - Created on 6/19/2024

> Original URL: https://github.com/facebook/react/issues/29947

## Description

I have created a sample React application in which an const array variable is populated with values in rowDataBoundEvent function, but when I try to access the array variable value in another function `dataBoundEvent` in console it comes empty. This issue occurs only in Firefox but works fine in both Chrome and Edge browsers.

React version: 18.1

## Steps To Reproduce

1. In the following sample, I have displayed the array variable value once the dataBound event is triggered.
2. You can find that the arrayVal variable gives empty value.

Link to code example: https://stackblitz.com/edit/react-jmv77v-ycnlvj?file=index.js

Firefox:
![image](https://github.com/facebook/react/assets/93654184/a6cb3b0f-2c46-4087-a12b-5ae374e72a05)

Edge:
![image](https://github.com/facebook/react/assets/93654184/2c60cd62-cfd4-4344-9395-2f8c3176d876)

## The current behavior
The array variable value populated in a function does not reflect the value updated in another function in Firefox

## The expected behavior
The array variable value populated in a function should reflect the value updated in another function in Firefox similar to chrome and edge browsers.

