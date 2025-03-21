# Bug: SetState Calls not being batched inside Promise calls/micro Task

> Issue #30605 - Created on 8/6/2024

> Original URL: https://github.com/facebook/react/issues/30605

## Description

`setState` calls are generally batched in React. However, in a case where setState calls occur inside a native event handler that also includes a microTask (Promise), the batching behaviour changes. When a setState is executed first in the synchronous part of the handler, followed by a microTask operation which includes a state update, and then another setState is executed after the microTask, these setState calls are not batched together as one might expect. the stateUpdate inside the Promise call does not get batched.


React version: 18.3.1

## Steps To Reproduce

I am attaching a code Sandbox below to reproduce the same, where you can just run the code and see the Count Value rendered which does not resemble with the Way react should behave.

Link to code example:

https://stackblitz.com/edit/vitejs-vite-5lvqjx?file=src%2FCounter.tsx

## The current behaviour

if we look closely, currently the count is getting set to 2, which proves the point, that state updates inside the Promise call are not being batched.

https://github.com/user-attachments/assets/4a686d8d-5815-4c6c-bc5a-b7b638c85bd8




## The expected behaviour
the state update call inside the Promise should have been batched which would have made the count value to be 1 on the increment click.
