# [Compiler Bug]: Optimization Fails with Nested Method Shorthand Syntax in Components

> Issue #31180 - Created on 10/11/2024

> Original URL: https://github.com/facebook/react/issues/31180

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/hlege/react-compiler-bug

### Repro steps

If a nested method shorthand syntax is used in a component that returns an arrow function, it will prevent React's compiler optimizations. However, if the arrow function syntax is used instead, the optimizations work as expected.

```jsx
import React from 'react';

const TestContext = React.createContext({});

export function Test() {
    const context = {
        foo: 'fsd',
        testFn() {  // if it is an arrow function its work
            return () => 'test'; // it will break compile if returns an arrow fn 
        },
        bar: 'bar'
    };

    return (
        <TestContext.Provider value={context}>
            <div>Not Compiled </div>
        </TestContext.Provider>
    );
}
````

The `returnsNonNode(...)` is not skipping the nested function and detects the return type of it, causing the compiler to mistakenly interpret the Functional Component as non-Component functions.

[Link for code](https://github.com/facebook/react/blob/7b7fac073d1473df839a1caf8d0444c32bf4de49/compiler/packages/babel-plugin-react-compiler/src/Entrypoint/Program.ts#L968)

Tested with:
`babel-plugin-react-compiler` version: 0.0.0-experimental-e504e66-20241010

Note:
In playground it is work. 

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-70fb1363-20241010
