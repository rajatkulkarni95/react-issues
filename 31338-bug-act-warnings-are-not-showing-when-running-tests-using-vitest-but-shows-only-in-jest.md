# Bug: act warnings are not showing when running tests using Vitest but shows only in Jest. 

> Issue #31338 - Created on 10/24/2024

> Original URL: https://github.com/facebook/react/issues/31338

## Description

I have a test that should trigger an act warning. When trying to run Jest and rendering the component it shows the act warnings as expected but when running vitest no act warnings are shown, I tried playing around with configuration file to see if console warnings/errors are disabled somehow but no luck.

I reached out to the Vitest team and it seems like nothing is happening from the vitest side and I'm suspecting that React is expecting jest to log this error somehow. https://github.com/vitest-dev/vitest/issues/6782


React version: 18.3.1

## Steps To Reproduce

1. Create a very simple react counter component with async state 
```
import React, { useState, useEffect } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Simulate an async state update, like a network request.
    const timer = setTimeout(() => {
      setCount(count + 1);
    }, 5000);

    return () => clearTimeout(timer);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```
2. Run the following test:
```
import Counter from "../comp";
import { it } from "vitest";
import { createRoot } from "react-dom/client";

it("Counter", () => {
  const container = document.createElement("div");
  createRoot(container).render(<Counter />);

  const buttonElement = container.querySelector("button"); 
  buttonElement?.click();
});
```


The code example link below shows the same code examples above, just run `npm run test`.

Link to code example: https://stackblitz.com/edit/vitest-dev-vitest-zk9hnz?file=test%2Fcounter.test.tsx



## The current behavior
Test succeeds, no act warnings.

## The expected behavior
Test succeeds with act warnings like Jest.

