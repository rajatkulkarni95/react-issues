# Bug: promises passed to server actions block on promise parameters

> Issue #28510 - Created on 3/7/2024

> Original URL: https://github.com/facebook/react/issues/28510

## Description

React version: 18.2.0

## Steps To Reproduce

1. Create a server action that takes a promise parameter `p`:
   ```js
   "use server";
   
   export async function serverAction(p: Promise<void>) {
     console.log(p);
     const t1 = new Date();
   
     await p;
   
     const t2 = new Date();
   
     console.log("elapsed", t2.valueOf() - t1.valueOf());
     return {
       t1,
       t2,
     };
   }
   ```
2. Pass `new Promise((r) => setTimeout(r, 10_000))` to that server action.
3. Expect that the action begins running immediately, then blocks on the promise, and reports an elapsed time of approximately 10 seconds.

Link to code example:

https://codesandbox.io/p/devbox/next-14-0-3-forked-7q86s7?file=%2Fapp%2Factions.ts%3A4%2C18&workspaceId=958ee911-ec8f-4ca3-9ce1-668005ecaeb8

## The current behavior

Serialization of promises is synchronous and blocking.

## The expected behavior

That a promise could be passed to a server action and resolved asynchronously, e.g., as a cancellation token.
