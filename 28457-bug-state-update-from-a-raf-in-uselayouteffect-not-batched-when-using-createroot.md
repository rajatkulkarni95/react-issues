# Bug: state update from a rAF in useLayoutEffect not batched when using `createRoot`

> Issue #28457 - Created on 2/27/2024

> Original URL: https://github.com/facebook/react/issues/28457

## Description

Maybe a weird edge case, but this caused an unexpected visual change in our app when migrating a root from `ReactDOM.render`.

React version: 18.2.0

## Steps To Reproduce

1. Define a component that has some state, and a `useLayoutEffect` that modifies the state in a `requestAnimationFrame` callback. like: 

```jsx
function App() {
  const [message, setMessage] = React.useState("Loading...");

  React.useLayoutEffect(() => {
    requestAnimationFrame(() => {
      setMessage("Ready");
    });
  });
  return <p>{message}</p>;
}
```
2. Mount the component using `ReactDOM.render`, and you will never observe the component with its initial state ("Loading..."). Only the updated state ("Ready").
3. Mount the component with `createRoot` and `root.render`, and you will observe the component render twice. Once with the initial state ("Loading..."), then with the updated state ("Ready").

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codepen.io/mxmul/pen/abMexLe

[react-batching.webm](https://github.com/facebook/react/assets/3022244/5a1e3238-5b30-4b74-b796-01024dae07b5)

## The current behavior

Two renders - once with the initial state, and a second with the updated state.

## The expected behavior

A single render with the updated state. This seems to be the behavior before React 18.

