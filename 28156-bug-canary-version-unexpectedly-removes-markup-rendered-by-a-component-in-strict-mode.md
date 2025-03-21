# Bug: Canary version unexpectedly removes markup rendered by a component in Strict Mode

> Issue #28156 - Created on 1/30/2024

> Original URL: https://github.com/facebook/react/issues/28156

## Description

Our 3rd-party component, [DevExtreme Reactive Grid](https://devexpress.github.io/devextreme-reactive/react/grid/), works as expected in React 18.2 (dev mode with Strict Mode enabled). The Canary channel version 18.3.0 however, first renders the component to the DOM and displays it properly (simulating mount-unmount-mount as usual), but then suddenly removes the rendered markup, without any effects being destroyed or lifecycle methods called for class components. The component remains displayed in React Dev Tools. So, I believe there is probably a regression in React Canary 18.3.0.

You will note that the component uses freshly deprecated `defaultProps` property, hence some messages in the console, but it seems the issue has nothing to do with them.

React version: 18.3.0-canary-971b62f47-20240129

## Steps To Reproduce

1. Run the linked CodeSandbox;
2. See the empty page displayed because the component is first rendered and then removed. The component and its children are still displayed in React Dev Tools;
3. Change React version to 18.2.0 in package.json;
4. See the component properly displayed.

Link to the code example:

https://codesandbox.io/p/sandbox/distracted-visvesvaraya-forked-jlzg8s

## The current behavior

The component markup is removed from DOM after the component is rendered.

## The expected behavior

The component is displayed on the page.
