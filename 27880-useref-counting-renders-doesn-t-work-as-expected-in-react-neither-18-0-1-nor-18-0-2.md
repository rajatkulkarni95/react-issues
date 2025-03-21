# useRef: Counting renders doesn´t  work as expected in React neither 18.0.1 nor 18.0.2

> Issue #27880 - Created on 1/5/2024

> Original URL: https://github.com/facebook/react/issues/27880

## Description

I am trying to count each instance I type a letter into an input. In React 17.0.2 works fine: 1,2,3,4,... . But in React 18.0.1 and 18.0.2 the counting starts from 2 jumping over the number 1:    2,3,4,... 


React version: 18.0.1 and 18.0.2

## Steps To Reproduce

1.  Replace the App.js code with the code given below in a new React 18.0.1 and 18.0.2 project.
2. npm start and type letters into the input field. You will see the counting starts from 2 and not from 1 as it should be.


Code:
```js
import { useEffect, useRef, useState } from "react";

function App() {
  const [inputValue, setInputValue] = useState("");

  const ref = useRef(0);

  useEffect(() => {
    ref.current = ref.current + 1;
  });

  return (
    <>
      <input
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <p>{ref.current}</p>
    </>
  );
}

export default App;
```

## The current behavior

2,3,4...

## The expected behavior

1,2,3,4...
