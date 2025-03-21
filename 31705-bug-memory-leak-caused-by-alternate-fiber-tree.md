# Bug: memory leak caused by alternate fiber tree

> Issue #31705 - Created on 12/9/2024

> Original URL: https://github.com/facebook/react/issues/31705

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19

## Steps To Reproduce

```typescript
import React, { useState, useCallback } from "react";

const App = () => {
  const [obj, setObj] = useState<any>({});
  const [count, setCount] = useState(0);

  const refresh = useCallback(() => {
    const newObj = {
      buffer: new Uint8Array(100_000_000),
      count: count + 1,
    };
    setObj(newObj);
    setCount((pre) => pre + 1);
  }, [count]);

  return (
    <div>
      <button onClick={refresh}>new obj({count})</button>
    </div>
  );
};

export default App;
```

## The current behavior
<img width="732" alt="image" src="https://github.com/user-attachments/assets/503bfa91-0bae-46cd-a4d7-a103f8cd4e2f">

## The expected behavior
release the `memoizedState` / `baseState` of alternate fiber tree.

## Confusion
I know it's not a good way to store a big state using `useState`. But it's a bug or some feature?

