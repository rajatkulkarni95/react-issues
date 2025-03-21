# Bug: State updates are reordered across await in an effect in React 18.

> Issue #30890 - Created on 9/6/2024

> Original URL: https://github.com/facebook/react/issues/30890

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. Create an effect of the following form:
```javascript
useEffect(() => {
    (async () => {
        setStateA("foo");
        await someAsyncFunctionThatReturnsImmediately();
        setStateA("bar");
    })();
});
```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/react-dev-forked-9m77xd

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
React will render with the second state update first ("bar"), and then re-render with the first update ("foo"). This only happens when the awaited function returns immediately. If the awaited promise resolves at a later time, the state is updated in the expected order.

In the example, you can observe this happening by clicking the button and looking at the console ("BUG RENDERED!!!😱😱😱"), or by seeing a brief flash of red on the component as it renders inaccurately. The console message triggers every time, the red flash only occurs occasionally. In our actual app we're seeing the render occur every time. 

If you adjust the example to instead call `await optionalDelay(true)`, the state updates will be applied in order and the component will flash green.

## The expected behavior
The state updates should be applied in the order as specified in the code. This was the behavior in React 16, which can be tested in the sandbox.

This appears to be fixed in React 19.0.0-rc.0.

Previously reported in:
* #25129, which has a wonderfully concise repro https://codesandbox.io/p/sandbox/cocky-fermat-qoiel3.
* #24649, where this was mentioned as a [known issue](https://github.com/facebook/react/issues/24649#issuecomment-1511754282) but no tracking issue was given.

