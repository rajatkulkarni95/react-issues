# Bug: Context Provider not re-rendering when adding multiple arguments to a custom hook

> Issue #29054 - Created on 5/14/2024

> Original URL: https://github.com/facebook/react/issues/29054

## Description

React version: ^18.2.0

## Steps To Reproduce
1. Create a custom hook that accepts a single argument and fetches data based on that argument.
2. Use the custom hook in a Context Provider component and verify that the provider re-renders when the data updates.
3. Modify the custom hook to accept multiple arguments (e.g., two arguments).
4. Use the modified custom hook in the Context Provider component with multiple arguments.
5. Update the data related to the arguments and observe if the Context Provider re-renders correctly.

Link to code example: https://gist.github.com/Slyracoon23/b1b3f5225ad56e2a84d00e2efd2b3c64
Loom video: https://www.loom.com/share/1239ea003063459d9687a9804f998c5b

## The current behavior
- When using a single argument in the custom hook, the Context Provider re-renders correctly when the data updates.
- However, when using multiple arguments in the custom hook, the Context Provider does not re-render properly when the data updates.

## The expected behavior
- The Context Provider should re-render correctly whenever the data fetched by the custom hook updates, regardless of the number of arguments passed to the hook.

## Additional Information
- The issue seems to be related to how React handles re-rendering when multiple arguments are passed to a custom hook used within a Context Provider.
- The problem is not specific to any particular data fetching library or API, but rather a general React behavior.

## Possible Causes
- React may not be correctly detecting changes in the custom hook's dependencies when multiple arguments are used.
- The way the custom hook is implemented or used within the Context Provider might be causing the re-rendering issue.

## Suggested Solutions
- Investigate how React handles re-rendering when multiple arguments are passed to a custom hook.
- Review the implementation of the custom hook and ensure it correctly handles multiple arguments and updates the data accordingly.
- Verify that the Context Provider is correctly consuming the data from the custom hook and re-rendering when changes occur.

## Additional Context
- The relevant code snippets for the Context Provider and custom hook are provided below:

```tsx
// ContextProvider.tsx
// ...

const { data, error, loading } = useCustomHook(arg1, arg2)

// ...
```

```tsx
// useCustomHook.tsx
// ...

export const useCustomHook = (arg1: string, arg2: string) => {
  // ...
}

// ...
```

