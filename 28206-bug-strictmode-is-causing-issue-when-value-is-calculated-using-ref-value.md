# Bug: StrictMode is causing issue when value is calculated using ref value

> Issue #28206 - Created on 2/2/2024

> Original URL: https://github.com/facebook/react/issues/28206

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

When using StrictMode, render and useEffect are wrong when calculating a value based on some ref.
For example with this code:
```ts
function useDiff(items: number[]): boolean {
  const ref = useRef<number[]>(items); // reference to the previous value of items

  let hasDiff = false;
  const prev = ref.current;
  const all = new Set(prev.concat(items));
  all.forEach((name) => {
    if (!prev.includes(name) || items.includes(name)) {
      hasDiff = true;
    }
  });
  ref.current = items;

  useEffect(() => {
    if (hasDiff) {
      console.log("There are some differences !"); // This never gets logged when using StrictMode
    }
  });

  return hasDiff; // this is always false when using StrictMode
}
```

React version: 18.2

## Steps To Reproduce

1. See code sandbox example
2. Click on "Add" button
3. It should display `hasDiff = true` and log `There are some differences !` in the console

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/happy-antonelli-ysr36h?file=%2Fpackage.json%3A13%2C29

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

When clicking the "Add" button wrong value is being rendered (`hasDiff = false`), and `console.log` inside `useEffect` is not triggered.

## The expected behavior

Removing `StrictMode` will change the behavior like so:
When clicking the "Add" button `hasDiff = true` is being rendered, and `console.log` inside `useEffect` is triggered.
I expect the code to work the same when using `StrictMode`.

