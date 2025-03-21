# A lengthy task in a resource-intensive application.

> Issue #27770 - Created on 12/1/2023

> Original URL: https://github.com/facebook/react/issues/27770

## Description

I have a highly-loaded SPA application with frequent store updates and, consequently, a high frequency of interface updates. Calculating data takes a significant amount of time, resulting in a long task of around 70ms. Additionally, due to changes in the pull request - https://github.com/facebook/react/pull/26512, a microtask is executed with an update, also taking a considerable amount of time.

The total task execution time is 117ms. For me, it would be better to move flushSyncCallbacks into a separate task rather than running it as a microtask.

Is it possible to provide control over scheduling processing? For instance, allowing the replacement of the use of queueMicrotask with something custom, perhaps as a parameter in createRoot, or similar to what is done in react-redux (https://github.com/reduxjs/react-redux/blob/master/src/utils/batch.ts).

I have some ideas for implementation and can create a pull request.

<img width="584" alt="image" src="https://github.com/facebook/react/assets/6467881/97bb9bd7-8514-4788-9b2d-c5ef65de6218">

React version: 18.2.0

## The current behavior

A long task in conjunction with a microtask.

## The expected behavior

The code executed in a microtask runs in a separate task.
