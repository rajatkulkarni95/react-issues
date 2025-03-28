# Bug: Change status variable type

> Issue #31467 - Created on 11/9/2024

> Original URL: https://github.com/facebook/react/issues/31467

## Description

I noticed the status variable in the ReactPromise function of the ReactFlightClient file, is of type any.

If the status is always of type String, it would be a good idea to replace `any` with `string`. This helps provide stronger type checking, reduces the risk of bugs, and improves code readability.

[ReactFlightClient.js](https://github.com/facebook/react/blob/main/packages/react-client/src/ReactFlightClient.js)
line: 206

![function](https://github.com/user-attachments/assets/34d5db34-4d29-4f3b-810f-7518c964a99b)

