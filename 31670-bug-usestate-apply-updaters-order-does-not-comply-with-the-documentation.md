# Bug: useState apply updaters order does not comply with the documentation

> Issue #31670 - Created on 12/4/2024

> Original URL: https://github.com/facebook/react/issues/31670

## Description

React version: 16 & 18

## Steps To Reproduce
1. Call setState(functional updater) twice
2. One of the updater will be calculated before re-render.

Link to code example: https://codesandbox.io/p/sandbox/quizzical-hugle-wsp7zh

## The expected behavior
As per the [documentation of setState](https://react.dev/reference/react/useState#setstate),
> If you pass a function as nextState, it will be treated as an updater function. It must be pure, should take the pending state as its only argument, and should return the next state. 
> **React will put your updater function in a queue and re-render your component. During the next render, React will calculate the next state by applying all of the queued updaters to the previous state.**

Expected behaviour is,
1. click on the button
2. enqueue two updater actions
3. the App component re-renders
4. (when visiting useState) apply two actions
5. get the updated new value
 
## The current behavior
However the current behavior is,
1. click on the button
2. one of the actions is calculated IMMEDIATELY, the rest are enqueued.
3. the App component re-renders
4. (when visiting useState) apply the remaining actions
5. get the updated new value

![image](https://github.com/user-attachments/assets/8a0ff342-b155-44bb-884d-9c44a13a4db9)


## Note
Only the *first* time not complying. From the second time it works expectedly.
![image](https://github.com/user-attachments/assets/f80e96ef-0396-452e-9e05-f4c922f15f90)

