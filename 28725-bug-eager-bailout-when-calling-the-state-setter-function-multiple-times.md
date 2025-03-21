# Bug: Eager bailout when calling the state setter function multiple times

> Issue #28725 - Created on 4/3/2024

> Original URL: https://github.com/facebook/react/issues/28725

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

I understand from several issues (#20817 #28287) that React implements an **eager bailout** for state updates to optimize performance. So I ran some tests with simple examples, and I had some questions about **calling the state setter function multiple times** for a single event. Below is a detailed explanation of that.

React version: 18.0.0

## Steps To Reproduce

1. Initialize the state using `useState` hook:
```js
const [number, setNumber] = useState(0);
```
2. Define click event handlers that call `setCount` multiple times:

```js
// case 1
const handleClick = () => {
  setCount(0);
  setCount(0);
  setCount(0);
};
``` 

```js
// case 2: includes changes
const handleClick = () => {
  setCount(0);
  setCount(1);
  setCount(0);
}
```

3. Click the button to trigger the event handler.


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: [CodeSandbox](https://codesandbox.io/p/sandbox/setstate-parent-only-d4xfty?file=%2Fsrc%2FApp.js%3A20%2C1)

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

The two cases behaved differently when the button was clicked. In the first case, the parent component did not render at all, and of course, its child components did not render either. In contrast, in the second case, only the component rendered. (Child components did not render.)

I'm wondering why the parent component re-renders in the second case when the state is eventually set to 0 (to initial state). Does the parent component have to start the rendering process to figure out if it can quit early? Why?

## The expected behavior

Since React batches updates for an event, it seems to be more efficient to compare only the last update and the previous state? In other words, shouldn't it be possible to avoid re-rendering the parent component for the second case as well? 

My understanding of the internally implemented code might be incomplete, so please let me know if there are any errors or misunderstandings in my explanation.
