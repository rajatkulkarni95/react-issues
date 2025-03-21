# Bug: Tab focus does not move to the correct element in Firefox when unmounting on key down

> Issue #27847 - Created on 12/20/2023

> Original URL: https://github.com/facebook/react/issues/27847

## Description

When unmounting a component upon tabbing out of it (using onKeyDown), focus should go to the next element in DOM order. However, in Firefox, focus goes to the parent.

React version: 18.2.0

## Steps To Reproduce

1. Create four buttons
2. Have the third button have style "display: none"
3. Add onFocus to the second button to make the third button appear
4. Add onKeyDown on the third button to make the third button disappear if the key pressed is Tab

Link to code example: https://codesandbox.io/p/sandbox/reactjs-playground-forked-wdsd4f

## The current behavior
In Firefox, tabbing away from the third button moves focus back to the first button.

## The expected behavior
In all other browsers, focuses moves to the last button.

Here is a codesandbox with the same situation but in vanilla JS, which works correctly in Firefox: https://codesandbox.io/p/sandbox/javascript-forked-gplg3h

