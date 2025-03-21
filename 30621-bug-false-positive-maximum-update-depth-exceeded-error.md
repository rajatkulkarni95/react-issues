# Bug: False positive maximum update depth exceeded error

> Issue #30621 - Created on 8/7/2024

> Original URL: https://github.com/facebook/react/issues/30621

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. A functional component with a slow render method of around 3 milliseconds
2. Three states: `a`, `b`, `c`
3. One effect that runs when state `a` changes which changes `b`
4. Another effect that runs when state `b` changes which changes `c`
5. An input which changes state `a`
6. Type at least 25 characters into the input with a delay of 1 millisecond between each character

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/max-depth-exceeded-false-positive-nrjtft?file=%2Fsrc%2FApp.tsx%3A52%2C40

```typescript
import { forwardRef, useEffect, useRef, useState } from "react";
import "./styles.css";

// This needs to be at least 25 characters long.
const text = "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz";
// This needs to be less than the renderTime.
const typingDelay = 1;
// This needs to be at least 3 milliseconds.
const renderTime = 10;

export default function App() {
  const ref = useRef<HTMLInputElement>(null);

  useEffect(() => {
    const input = ref.current;
    let timeoutId: number | undefined = undefined;

    if (input) {
      const typeCharacter = (index: number) => {
        if (index < text.length) {
          const char = text[index];
          console.log("Typing character", char, index + 1);
          input.dispatchEvent(
            new InputEvent("input", {
              bubbles: true,
              composed: true,
              detail: 0,
              view: window,
              data: char,
              inputType: "",
            })
          );
          input.value += char;
          timeoutId = setTimeout(() => typeCharacter(index + 1), typingDelay);
        }
      };

      typeCharacter(0);
    }

    return () => clearTimeout(timeoutId);
  }, [ref.current]);

  return (
    <div className="App">
      <h1>React - Maximum Depth Exceeded False Positive</h1>
      <h2>Check the console for errors</h2>
      <SlowInput ref={ref} />
    </div>
  );
}

const SlowInput = forwardRef<HTMLInputElement>(function MyInput(props, ref) {
  const [unused, setUnused] = useState({});
  const [used, setUsed] = useState({});
  const [name, setName] = useState("");
  useEffect(() => setUnused({}), [used]);
  useEffect(() => setUsed({}), [name]);

  spin(renderTime);

  return <input onInput={(e) => setName(e.currentTarget.value)} ref={ref} />;
});

function spin(ms: number) {
  const start = Date.now();
  while (Date.now() - start < ms) {
    // Spin!
  }
}
```

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

After typing the 25th character (or sometimes a few later) the following error appears in the console:
```
 Warning: Maximum update depth exceeded. This can happen when a component calls setState inside useEffect, but useEffect either doesn't have a dependency array, or one of the dependencies changes on every render.
    at MyInput (https://nrjtft.csb.app/src/App.tsx:58:51)
    at div
    at App (https://nrjtft.csb.app/src/App.tsx:18:33)
```

Increasing the `typingDelay` to `10` and decreasing the `renderTime` to `1` causes the error to go away.

## The expected behavior

This error is a false positive and should not be shown.
