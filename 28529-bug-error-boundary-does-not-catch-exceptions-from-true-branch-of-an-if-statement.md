# Bug: error boundary does not catch exceptions from 'true' branch of an if-statement

> Issue #28529 - Created on 3/9/2024

> Original URL: https://github.com/facebook/react/issues/28529

## Description

When wrapping a standard-implementation error boundary around a component, as per [https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary), and the wrapped component throws an exception from within an if-statement's conditional branch, it weirdly only catches the exceptions thrown on the `false` branch, but ignores those on the `true` branch.

React version: 18.2.0

## Steps To Reproduce

1. See the code example (also available in the TS playground link below)
2. See the instructions in the comments of the code example

```typescript
import { FunctionComponent, useEffect, useRef, useState } from "react";

const Weird: FunctionComponent = () => {
    const [version, setVersion] = useState<number>(0);
    const renderCount = useRef<number>(0);
    const condition = useRef<number>(0);

    console.info(`renderCount=${renderCount.current++}, version=${version}, condition=${condition.current}`);

    useEffect(() => {
        const id: NodeJS.Timeout = setTimeout(() => setVersion(i => i + 1), 1_000);
        return () => clearTimeout(id);
    }, []);

    // How to test this example:
    // 1. run the code and observe that it works as expected: the error boundary catches the exception
    // 2. change 'errorBoundaryCatchesError' to 'false'
    // 3. comment throwing line marked with "scenario a" below
    // 4. uncomment the throwing line marked with "scenario b" below
    // 5. run the code again to observe that the exception does not get caught by the error boundary anymore
    const errorBoundaryCatchesError: boolean = true;

    if (version === 1) {
        const testCondition: number = errorBoundaryCatchesError ? 1 : 0;
        if (condition.current++ === testCondition) {
            // scenario b - true branch
            // throw new Error("ignored error");
        } else {
            // scenario a - false branch
            throw new Error("caught error");
        }
    }

    return <div>Hello</div>;
}

export default Weird;
```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: [Typescript Playground](https://www.typescriptlang.org/play?#code/JYWwDg9gTgLgBAbzgMQK4DsDGNgXQYQnDwFN0YAaOVAZxIFEAzRk7K2kgJRMfboGUYAQxgk4AXziMoROACIoJIdjkBuAFDrMeGvADqJYFAAmALhQZsuAkUjoy8ALxwAFAEo4jgHyJ1cf3Da6LpwANoAbiRQNNZUdDAAalExeAC6ntQCwqIAPOioIABGUV4uAAxuGgGBOvCK6MZRhBhOmVw8eQXFUKUVVQFBIUHGwDh4GRzcjJ1FJeWVmtWDEAA2JAB0wOiMEC4ABvWNUM3kjgAkCIdNEC3rmKhQ9TAA1M-iVJHR1ucInyno7xqDVG3wuwxBeDuDye4j2Cz8AQ4TBY2Bc7k8PgQCOq-kG8GAZjgADkII0AFL8dYAFVAJBurXiNJAdNQMDRHm8cHiSS+eBcwAxcAFzzgAEY3FRRQB9MqyhY4gKKGAPdCuDk+TBrIRQJkstkE+UBQGhVLw6oAenNcAAEhAAO5wGAQR0kEIwAAWwBocBIAA8hOA1qZsXBLWL1nAoBhHe6xNpGnAhA04BBCnQoJEYyIhfA7dAANbeoTev1gViiQkesRRGRQOCFG4NbUAT0CIkwse9VZ9vswJDAY3QIbDACYIx2kwBzMQAchr0AAQo3jC38O3O-RHtAZ47nTPGEIVnQZ8OrQBmcdEZnkGMyO1bSdwFZbMQgbX5kjGOD3j3yGh99BtVwRM5HrEgVntU84AAFgjSwrwcGMxA9O8HyfF84DfKAPy-H93T-ACgOdQpQOKCC7SggBWCMo1Vbt4zEIRJyELZdxTNMokzD1s27P0+wHaw4GMCBXTgdAIHgad4EwIRUEnd14EKVteK3OsGwwFcoFbJNmxAaASBDPEfVUpcNNXddXU3WtzAbVYlFVZwYCjEgNBDYBGFcP5BMcHyxQ8LEFVxWoXV0QhgUHcx8lmOtnHnKBTKbLS1xgDtLNUuAAH4xTgcwyn6BV3NccFByhR4HFeTxfNEUK8BGQd-JDQLQytf8yCI+s4AAWkdZz6ygJMO0awKwxQ+0xJIB0rOgFw5GASdxMUL84rkQ0FUkcC6F8JqLRawioGAoQuqkQ9NsKfqsHdIaFVGh17Em1SZpkuSFOM2sVvynFxBDL6QyVFU4ByEZwi8a1wIgnJzSBrwNB+0toHgRoD1QFZ9EMExVCAA)

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
When the above function component, `Weird`, is wrapped into a standard-implementation error boundary, like this:
```typescript
<ErrorBoundary>
   <Weird />
</ErrorBoundary>
```
...the exception thrown in the component only gets caught by the error boundary if it is thrown from the `false` branch of the if-statement, but not if thrown on the `true` branch.

## The expected behavior
Independently on which branch the exception is thrown from, it should get caught in both cases.
