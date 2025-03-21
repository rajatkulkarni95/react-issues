# Bug: useEffect fires synchronously even though it is not the result of a discrete input 

> Issue #31567 - Created on 11/17/2024

> Original URL: https://github.com/facebook/react/issues/31567

## Description

`useEffect` fires synchronously and blocks painting new UI to screen even though it is not the result of a discrete input.

React version: 18.3.1

## Steps To Reproduce

1. setState inside a setTimeout
2. inside useEffect callback wait for 10_000ms

```jsx
import { useState, useEffect } from "react";

const sleep = (time) => {
  const wakeUpTime = Date.now() + time;
  while (Date.now() < wakeUpTime) {}
  console.log(time + "ms passed");
};

export default function App() {
  const [text, setText] = useState("Hello");

  useEffect(() => {
    setTimeout(() => {
      setText("Bonjour");
    }, 1000);
  }, []);

  useEffect(() => {
    if (text === "Bonjour") {
     // "Bonjour" text will have to wait for 10000 ms to be shown on screen 
      sleep(10000);
    }
  }, [text]);

  return (
    <div className="App">
      <h1>{text}</h1>
    </div>
  );
}
```

Link to code example:
https://codesandbox.io/p/sandbox/7zqlmm

## The current behavior
After `setText("Bonjour")` from a `setTimeout`, it has to wait for 10000ms to be shown on screen.

## The expected behavior
After `setText("Bonjour")` from a `setTimeout`, it's shown immediately on screen, as the doc says React only flush synchronously useEffect resulting from discrete events like clicks.

Reference:
- https://github.com/facebook/react/pull/21150
- https://github.com/reactwg/react-18/discussions/128

I don't know if this is a bug or an undocumented behavior. How is the `setState` inside `setTimeout` a discrete input ?

