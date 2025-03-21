# Bug: Strict mode effect cleanup order doesn't match normal unmount

> Issue #30765 - Created on 8/21/2024

> Original URL: https://github.com/facebook/react/issues/30765

## Description

React version: 18.2 or 18.3

## Steps To Reproduce

1. Use this code:

```jsx
import { useState, useEffect } from "react";

export default function App() {
  const [show, setShow] = useState(false);
  return (
    <>
      <button onClick={() => setShow(!show)}>Toggle</button>
      {show ? (
        <A>
          <B />
        </A>
      ) : (
        "Not showing"
      )}
    </>
  );
}

function A({ children }) {
  useEffect(() => {
    console.log("parent effect");

    return () => console.log("parent effect cleanup");
  });
  return <div>{children}</div>;
}

function B() {
  useEffect(() => {
    console.log("child effect");
    return () => console.log("child effect cleanup");
  });
  return null;
}
```


2. Observe the logs you get:
```
// Click to show
child effect
parent effect
child effect cleanup
parent effect cleanup
child effect
parent effect
// Click to hide
parent effect cleanup
child effect cleanup
```

Link to code example: https://codesandbox.io/s/sleepy-bhabha-q5tfnt?file=/src/App.js

## The current behavior

Notice that during the strict mode cycle, the child effect cleanup runs before the parent's. But during actual unmounting, the child effect cleanup runs **after** the parent's.

## The expected behavior

I expected the behavior to match.

## Why does this matter

From my investigations:

1. The expected behavior is not documented (neither for strict mode nor for normal unmount). I have searched for `order` and `child` on this page: https://react.dev/reference/react/useEffect
2. From past issues it seems that the React team has strong opinions on what the order should be, although I'm not clear on what that order is.

The scenario we're trying to implement is for the parent to provider authentication state and for children to be subscribed and depend on this external authentication state.

Ideally we'd want:
1. the parent's effect to run first (set authentication credentials), then children (subscribe)
2. the child effect cleanup to run first (unsubscribe), then parent (clear authentication credentials)

We achieved the first with useLayoutEffect (isomorphic for SSR) in parent, and useEffect in child.

But now I'm realizing there might be no easy way to achieve the second, without deferring the cleanup to another tick while avoiding racing with another render.

Also note that from my testing this popular SO answer on this topic is wrong: https://stackoverflow.com/a/55028488/1526986
