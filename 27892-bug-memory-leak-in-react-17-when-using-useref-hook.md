# Bug: Memory Leak in React 17 when using useRef Hook

> Issue #27892 - Created on 1/8/2024

> Original URL: https://github.com/facebook/react/issues/27892

## Description

React version: 17.0.2
React-dom version: 17.0.2

## Steps To Reproduce

- Create a React component View that uses useRef to create a ref and passes it to a div element.
- In another component App, include a toggle button that can mount and unmount the View component.

Here is the code
```
import React, { useState } from "react";

export default function App() {
  const [visible, setVisible] = useState(true);

  return (
    <div className="App">
      <button onClick={() => setVisible(!visible)}>toggle view</button>
      {visible ? <View /> : null}
    </div>
  );
}

const View = () => {
  const ref = React.useRef<HTMLDivElement>(null);

  return <div ref={ref}>this view is visible</div>;
};

```

- Open the provided demo in the Edge browser: [React Memory Leak Demo](https://codesandbox.io/p/sandbox/react-memory-leak-useref-mngn43).
- Click the "toggle" button to unmount the View component.
- Use Edge's Detached DOM tool and click collect garbage button and then click get detached elements,.
- You can see the div element to be detached element.![image](https://github.com/facebook/react/assets/2008850/47393bf0-9313-4559-a2bc-8bda4716f0e3)



Link to code example:
https://codesandbox.io/p/sandbox/react-memory-leak-useref-mngn43


## The current behavior
The DOM element has not been garbage collected.

## The expected behavior
The DOM element has been garbage collected.

