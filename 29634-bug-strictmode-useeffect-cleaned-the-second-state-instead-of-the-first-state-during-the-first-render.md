# Bug: StrictMode: useEffect cleaned the second state instead of the first state during the first rendering

> Issue #29634 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29634

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce
```tsx
import { useEffect, useState } from "react";

let stateId = 0;
const createState = () => {
  const objId = ++stateId;
  console.log("create state", objId);
  return {
    destroy: () => {
      console.log(`state ${objId} destroyed`);
    },
  };
};
export default function App() {
  const [state] = useState(createState);

  useEffect(() => {
    return () => {
      state.destroy();
    };
  }, [state]);

  return <div className="App"></div>;
}

```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/damp-wildflower-x47s5m?file=%2Fsrc%2FApp.js%3A39%2C7

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
console output:
```
create state 1
create state 2
state 2 destroyed
```
finally I got a destroyed state 2

## The expected behavior
```
create state 1
state 1 destroyed
create state 2
```
or?
```
create state 1
create state 2
state 1 destroyed
```
I will get a usable state 2
