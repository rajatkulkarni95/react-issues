# Bug: Error Recovery Mechanism Overwriting Initial Rendering Errors in Concurrent Mode

> Issue #30157 - Created on 7/1/2024

> Original URL: https://github.com/facebook/react/issues/30157

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:18

I have encountered an issue with the error recovery mechanism in Concurrent Mode (React 18's Concurrent Features), where initial rendering errors seem to be overwritten by subsequent errors triggered in side effects, making it difficult to debug and trace the original error.

## Steps To Reproduce

1.Create a component that intentionally throws an error during rendering.
Include a side effect (e.g., data fetching or model updating) that only triggers an error when React attempts to recover from the initial rendering error.
2.The Main component throws an error during rendering.
The useOnce hook calls a function which updates a global variable and throws an error on subsequent updates.

```
import React, { useRef, Component } from "react";

let a = null;

const updateA = () => {
  console.log("updateA");
  if (a) {
    throw "a has updated";
  }
  a = 1;
};

function useOnce(callback) {
  const hasRun = useRef(false);
  if (!hasRun.current) {
    callback();
    hasRun.current = true;
  }
}
export default function Main() {
  useOnce(() => {
    updateA();
  });
  throw "1111111";

  return null;
}
```
<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Get error "a has updated"
## The expected behavior
Get error '1111111'

