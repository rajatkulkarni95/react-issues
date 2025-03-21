# [DevTools Bug] Highlighting Occurs Without Actual Re-Rendering

> Issue #31638 - Created on 11/27/2024

> Original URL: https://github.com/facebook/react/issues/31638

## Description

### Website or app

https://stackblitz.com/edit/vitejs-vite-sm1mvc?file=src%2FApp.tsx&terminal=dev

### Repro steps

I’ve encountered a confusing behavior in React DevTools and would like to clarify whether this is expected or a potential bug.

In the following code, I’m using react-tracked to manage state. When I click the button in the Counter component to increment the count, the TextBox component does not re-render (as expected, since it doesn’t depend on the count state). However, in React DevTools, the TextBox component is still highlighted as if it was re-rendering.

Here’s the code for reference:
```javascript
import { memo, useState, useEffect } from 'react';
import { createContainer } from 'react-tracked';

const useValue = () => useState({ count: 0, text: 'hello' });

const { Provider, useTracked } = createContainer(useValue);

const Counter = memo(() => {
  const [state, setState] = useTracked();
  const inc = () => {
    setState((prev) => ({ ...prev, count: prev.count + 1 }));
  };
  return (
    <div>
      count: {state.count} <button onClick={inc}>+1</button>
    </div>
  );
});

const TextBox = memo(() => {
  const [state, setState] = useTracked();
  const setText = (text: string) => {
    setState((prev) => ({ ...prev, text }));
  };
  console.log('render TextBox');
  useEffect(() => {
    console.log('effect TextBox');
  });
  return (
    <div>
      <input value={state.text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
});

const App = () => (
  <Provider> 
    <div>
      <Counter />
      <Counter />
      <TextBox />
      <TextBox />
    </div>
  </Provider>
);

export default App;
```

In the console, there’s no indication that the TextBox component re-rendered (console.log is not triggered), but the highlighting in DevTools suggests otherwise.

Could you help clarify why this is happening? Is this highlighting behavior in React DevTools expected, or is it a bug?

Thank you for your time and help!

### How often does this bug happen?

Every time

### DevTools package (automated)

_No response_

### DevTools version (automated)

_No response_

### Error message (automated)

_No response_

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
