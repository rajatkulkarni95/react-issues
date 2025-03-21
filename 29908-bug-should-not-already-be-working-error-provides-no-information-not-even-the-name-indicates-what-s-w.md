# Bug: "Should not already be working" Error Provides No Information (Not Even the Name Indicates What's Wrong)

> Issue #29908 - Created on 6/16/2024

> Original URL: https://github.com/facebook/react/issues/29908

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
18.3.1

## Steps To Reproduce

1. Write a test in React Testing Library
2. Run it
3. Get an error "Should not already be working" when testing library clicks on something (even a button with no `onClick`)
4. Have no clue what's going on or how to resolve

## Link to code example:

Unfortunately the code involves like ten component files, a test file, some test helper files, etc. which I can't include here.  Really, my code example isn't important to the ticket, but for reference the key bit is:

    import userEvent, { UserEvent } from '@testing-library/user-event';
    // ... test stuff ...
    const user = userEvent.setup()
    const applyButton = getByText('Apply');
    // Log applyButton, confirm we did find an element
    user.click(applyButton)

Which results in:

> ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯ Uncaught Exception ⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
> Error: Should not already be working.
>  ❯ performConcurrentWorkOnRoot node_modules/react-dom/cjs/react-dom.development.js:25742:11
>  ❯ flushActQueue node_modules/react/cjs/react.development.js:2667:24
>  ❯ act node_modules/react/cjs/react.development.js:2582:11
>  ❯ node_modules/@testing-library/react/dist/act-compat.js:47:25
>  ❯ renderRoot node_modules/@testing-library/react/dist/pure.js:180:26
>  ❯ render node_modules/@testing-library/react/dist/pure.js:271:10
>  ❯ renderHook node_modules/@testing-library/react/dist/pure.js:318:7
>  ❯ Proxy.default src/myFile.test.tsx:7:41

because of some unknown code being tested (if I knew what code I'd happily paste it here ... but then I wouldn't need to file this ticket).

In general , when React tells you something is wrong, it always tell you **_what_** is wrong, to the best of its ability.  With many React errors you not only get a helpful error message, but there's even a link to a webpage with further info :)

With this error, the message tells you nothing useful, and even Googling tells you almost nothing (it has something to do with blocking actions inside `useEffect`?) 

React should (more politely) say:

>Hey dummy, you did X: that's wrong.  Let me make sure you understand why X is wrong, and also how you can fix it"

A "react error documentation link" would certainly be nice, but even just an improved error message would be helpful.

## The current behavior

> Error: Should not already be working.

With an unhelpful stacktrace that doesn't mention any of the files actually involved:

 ❯ performConcurrentWorkOnRoot node_modules/react-dom/cjs/react-dom.development.js:25742:11
 ❯ flushActQueue node_modules/react/cjs/react.development.js:2667:24
 ❯ act node_modules/react/cjs/react.development.js:2582:11
 ❯ node_modules/@testing-library/react/dist/act-compat.js:47:25
 ❯ renderRoot node_modules/@testing-library/react/dist/pure.js:180:26
 ❯ render node_modules/@testing-library/react/dist/pure.js:271:10
 ❯ renderHook node_modules/@testing-library/react/dist/pure.js:318:7

## The expected behavior

This is an example; if I actually understood what this error meant, I'd write a PR with the new message, instead of this ticket.

> Error: You attempted to call a blocking action (eg. window.alert) inside a useEffect callback.  You must take this action out of the normal flow, for instance by putting it inside a setTimeout callback.

(And then, ideally, you'd get a stack trace that takes you to the `useEffect` that caused this problem.)
