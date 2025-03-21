# 🚀 Smart Render: A friendlier way to improve React’s performance & reduce bundle size (tree sharking built in) 🎯

> Issue #32360 - Created on 2/12/2025

> Original URL: https://github.com/facebook/react/issues/32360

## Description

React version: Affects all versions, but particularly relevant for React 19+.

## Steps To Reproduce

1. Create a simple React component using useState.
2. Update the state and observe that the entire component re-renders, even though only part of the UI actually changes.

Code example:


```
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  console.log("Component re-rendered");

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}


export default Counter;
```
👉 Problem: Every time count updates, the entire Counter component re-renders, even though only `<p>{count}</p>` needs to change.

## The current behavior
1. React re-renders the entire component when state changes, even if only a small part of the UI is affected.
2. Developers must manually optimize performance using memo(), useMemo(), and useCallback().
3. This leads to larger bundle sizes and harder-to-maintain code.

## The expected behavior
🚀 Only `<p>{count}</p>` updates, instead of re-rendering the whole component.
📦 No need for memo, useMemo, or useCallback, making React simpler to use.
⚡ Improved performance and smaller bundle size without extra manual optimizations.
✅ Use a single useState or useRef to keep things simple but effective.

Would love to hear thoughts from the React team and the community! 🚀🔥
