# 🐛 Bug: React 19

> Issue #32474 - Created on 2/25/2025

> Original URL: https://github.com/facebook/react/issues/32474

## Description

"In React 19, unexpected re-rendering was observed when state changes inside useEffect. This was not an issue in React 18."


Code (Problem status)

```js
import { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Effect triggered");
    setCount(count + 1); 
  }, []);

  return <p>Count: {count}</p>;
}

export default App;
```

Correct Solution for React 19

```js
import { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return <p>Count: {count}</p>;
}

export default App;

```

