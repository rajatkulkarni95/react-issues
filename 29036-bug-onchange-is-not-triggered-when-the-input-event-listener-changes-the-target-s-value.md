# Bug: onChange is not triggered when the 'input' event listener changes the target's value.

> Issue #29036 - Created on 5/10/2024

> Original URL: https://github.com/facebook/react/issues/29036

## Description

React version: 18.3.1

## Steps To Reproduce

1. Create a root component.
2. Insert an input tag that contains an `onChange` prop.
3. Call `useRef` to get the input.
4. In a `useEffect` call, add an event listener with "input" as the listener.
5. Observe how the `onChange` prop will not be triggered.

[Link to code example](https://codesandbox.io/s/eager-gates-fpnyvy?file=%2Fsrc%2FApp.js%3A13%2C7)

[Vanilla JavaScript example](https://codepen.io/timbo-dev/pen/ZENEXae?editors=1111)

### Current Behavior
After typing some characters into the input, the `input` event listener is triggered, changing the `target.value` property. However, for some reason, the `onChange` prop is not being triggered. If we comment out the line that changes the `target.value`, both listeners are triggered as expected.

## Expected Behavior
The `onChange` prop should be triggered after the `input` event listener changes the `target.value` property.
