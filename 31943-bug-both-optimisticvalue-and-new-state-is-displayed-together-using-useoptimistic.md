# Bug: Both optimisticValue and new state is displayed together using useOptimistic

> Issue #31943 - Created on 12/31/2024

> Original URL: https://github.com/facebook/react/issues/31943

## Description

Using the react Example given for useOptimistic hook in docs, an update in state passed to the hook should directly reset the optimisticState in one render.
Instead
1. It calls the updaterFn first, updates the optimisticState using new state and optimisticValue during one render cycle
2. resets optimisticState with new State in another render cycle.

As a result, both the new state and optimisticValue is rendered. Tried this in 20x slowdown

https://github.com/user-attachments/assets/3087c892-6f99-4ac5-b261-caf46bed343a

React version: 19

## Steps To Reproduce

1. Throttle CPU to 20x slowdown
2. Type some input in text box and press submit
3. See that the optimistic state is displayed and then it is pushed down for an instant along with the new state
4. Check console logs

<img width="1728" alt="Screen Shot 2024-12-31 at 1 28 14 PM" src="https://github.com/user-attachments/assets/fb2f8b96-a833-4d20-acb5-62a5f6218a2e" />


Link to code example:

https://codesandbox.io/p/sandbox/react-dev-forked-gmlxnr?file=%2Fsrc%2FApp.js&workspaceId=ws_QiCvK4c476hege6EDsXfpC

## The current behavior

When new state is passed to useOptimistic, 
1. It updates optimisticState by calling updaterFn with new state and optimisticValue
2. Component is rendered using this optimisticState (incorrect one)
3. Another update to optimisticState is done by resetting it to the new state
4. Component is rendered using this new optimisticState (correct one)

## The expected behavior

When new state is passed to useOptimistic, it should directly reset the optimisticState without calling the updater Fn
