# Bug: React refresh fails when component type is changed to memo or forward ref and vice versa

> Issue #30659 - Created on 8/12/2024

> Original URL: https://github.com/facebook/react/issues/30659

## Description

when Editing a JSX component, if we try to move from a normal React component to a memo Wrapped component,  or to a forwardRef wrapped, we cannot see any component rendered, but rather an error  ```Uncaught TypeError: Component is not a function```

this seems to be an issue with React refresh since if we try to reload the page, the component renders fine without any issue.

if we start with a code like below

```
import { forwardRef, memo } from "react";

export function Component() {
   return <h1>This is a component</h1>;
}

```

and then edit it to 

```

export const Component = memo(function Test() {
  return <h1>This is a memo component</h1>;
});

```

the error comes up




React version: 18.2.0

## Steps To Reproduce
[CodesandBoxLink](https://codesandbox.io/p/devbox/relaxed-clarke-6tty7m)

1. Visit the Sandbox URL
2. try editing the Component File
3. the initial render is of a normal Component
4. comment out the Normal component and uncomment the Memo wrapped component
5. it does not render instead if you check the console you would see an error
6. try commenting the Memo out and then check the ForwardRef, the same thing happens


Link to code example:
[CodesandBoxLink](https://codesandbox.io/p/devbox/relaxed-clarke-6tty7m)

if the codeSandBox is not able to reproduce the same due to some reason, try cloning the below repository
https://github.com/Biki-das/ReactRefreshBug

## The current behavior

https://github.com/user-attachments/assets/4e691ebf-38d1-4c05-9585-c5292aab5563


## The expected behavior
React refresh should have work and the component should have rendered.
