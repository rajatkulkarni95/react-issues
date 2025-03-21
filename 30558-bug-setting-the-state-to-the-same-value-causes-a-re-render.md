# Bug: Setting the state to the same value causes a re-render.

> Issue #30558 - Created on 8/1/2024

> Original URL: https://github.com/facebook/react/issues/30558

## Description

React version: 18.3.1

## Steps To Reproduce

1. Set the initial state to false.
2. Change the state to true.
3. Set the state to true once more.

Link to code example: [codesandbox](https://codesandbox.io/p/sandbox/rerendering-6njfxk)

```
import React, { useState } from "react";

const Child = () => {
  console.log("Child");
  return null;
};

export default function App() {
  const [state, setState] = useState(false);
  console.log("App");
  return (
    <>
      <button
        onClick={() => {
          setState(true);
        }}
      >
        click
      </button>
      <Child />
    </>
  );
}
```

## The current behavior
1. Print 'App' and 'Child' on the first rendering.
2. Clicking the <button /> prints 'App' and 'Child'.
3. Clicking the <button /> once more prints 'App'.

## The expected behavior
1. Print 'App' and 'Child' on the first rendering.
2. Clicking the <button /> prints 'App' and 'Child'.
3. Clicking the <button /> one more time results in no reaction.

I think this issue occurred because the previous current(now alternate)'s `lanes` was not cleared after reconciliation.

I confirmed that when the button was clicked a second time, the `lanes` was not `NoLanes`, so it did not compare with the previous state and immediately scheduled the rendering.
https://github.com/facebook/react/blob/v18.3.1/packages/react-reconciler/src/ReactFiberHooks.new.js#L2257-L2287

Since there were no updates during the rendering of the App component, it bailed out of rendering, so the children were not re-rendered.
https://github.com/facebook/react/blob/v18.3.1/packages/react-reconciler/src/ReactFiberBeginWork.new.js#L1047-L1050

However, if the `lanes` of the previous fiber had been cleared, such rendering would not have occurred.

I thought "If the state doesn't change, no re-rendering occurs", but I'm confused by the above result.

Is this a bug, or is there another reason for this behavior?
