# Bug: File input element missing cancel event handler

> Issue #27858 - Created on 12/28/2023

> Original URL: https://github.com/facebook/react/issues/27858

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. Add an `input` of type `file` with a `cancel` prop like this to a functional component: `<input type="file" cancel={cancel}>`
2. Observe error in console:
```Warning: Invalid value for prop `cancel` on <input> tag. Either remove it from the element, or pass a string or number value to keep it in the DOM. For details, see https://reactjs.org/link/attribute-behavior 
    at input
    at App```

Link to code example: [https://codesandbox.io/p/sandbox/keen-grothendieck-jcr72t?file=%2Fsrc%2FApp.js](https://codesandbox.io/p/sandbox/keen-grothendieck-jcr72t?file=%2Fsrc%2FApp.js)

## The current behavior
The `cancel` prop is considered an invalid prop on the `file` `input`.

## The expected behavior
`input` of type `file` includes `cancel` event listener. 
See documentation here: [https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#detecting_cancellations](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#detecting_cancellations)
See a working vanilla JS/HTML code example: [https://jsfiddle.net/snjm9p5d/](https://jsfiddle.net/snjm9p5d/)
The PR where this functionality was added to the HTML standard: [https://github.com/whatwg/html/issues/6376](https://github.com/whatwg/html/issues/6376)
