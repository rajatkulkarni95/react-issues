# Bug: Inconsistent behaviour based on object deconstruction.

> Issue #32375 - Created on 2/14/2025

> Original URL: https://github.com/facebook/react/issues/32375

## Description

Deconstructing an object and partially deconstructing it yields different behaviour. My best guess is this is a compiler issue.

React version: 19.0.0

## Steps To Reproduce

1. Make a boilerplate react app
2. Add a context and provider
```typescript
import React, { createContext, useState } from "react";

interface myState {
  someResult: number;
  setValue: Function;
}

export const MyContext = createContext<myState | null>(null);

export const MyContextProvider = ({
  children,
}: {
  children: React.ReactNode;
}) => {
  const setValue = (newVal: number) => {
    console.log(state.someResult); // <-- the behaviour of this line changes
    setState((prevState) => {
      return {
        ...prevState,
        someResult: newVal,
      };
    });
  };

  const [state, setState] = useState<myState>({
    someResult: 10,
    setValue: setValue,
  });

  return (
    <MyContext.Provider
      value={{
        ...state,
        // if this line is uncommented the console log above
        // will show the current value, otherwise it shows the initial
        // setValue: setValue,
      }}
    >
      {children}
    </MyContext.Provider>
  );
};
```

Link to code example:
(https://codesandbox.io/p/sandbox/inspiring-pike-9972nf)

## The current behavior
Depending on how `state` is passed to the `value` prop of the `Context.Provider` the behaviour inside the nested function changes.

## The expected behavior
Behaviour inside the nested function should not change.
