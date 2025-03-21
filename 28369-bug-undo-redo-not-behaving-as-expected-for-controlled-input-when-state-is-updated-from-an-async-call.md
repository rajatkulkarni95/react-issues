# Bug: Undo/Redo not behaving as expected for controlled input when state is updated from an async callback

> Issue #28369 - Created on 2/18/2024

> Original URL: https://github.com/facebook/react/issues/28369

## Description

Undo/Redo doesn't work correctly inside controlled input when its value is updated from an asynchronous callback or indirectly from its `onChange` handler.

React version: 18.1.0 & 18.2.0
Chrome 122.0.6261.49 (arm64)

Link to code example: 
1. https://stackblitz.com/edit/react-gtqvnu?file=src%2FApp.js
2. [codesandbox.io](https://codesandbox.io/p/sandbox/modest-dirac-n73zdf)

## Steps to reproduce
1. Navigate to either of the above links
2. Focus the input and enter some random text
3. Try undoing the changes (CMD+Z or Ctrl+Z or Edit>Undo)
4. Now notice that the value remains the same

## The current behaviour
Hitting CMD+Z doesn't fire the `onChange` event. Hitting it several times in succession may eventually bring the caret to the start of the input and sometimes appends the previous value onto the current value, eg.: `this is a testthis is a te`.

## The expected behaviour
Replace current value with previous value before last interaction with input.
