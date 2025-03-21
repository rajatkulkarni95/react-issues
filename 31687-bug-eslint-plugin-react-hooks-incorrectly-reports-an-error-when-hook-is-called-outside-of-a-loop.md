# Bug: [eslint-plugin-react-hooks] incorrectly reports an error when hook is called outside of a loop.

> Issue #31687 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31687

## Description

The following code triggers an ESLint error with the rule `eslintreact-hooks/rules-of-hooks` stating:  
> "React Hook 'useState' may be executed more than once. Possibly because it is called in a loop. React Hooks must be called in the exact same order in every component render."

However, the hook `useState` is not inside the loop, and there is no reason for the error to be thrown.

### React version:
React 19.0.0 (latest stable)
eslint-plugin-react-hooks 5.1.0 (latest stable)

## Steps To Reproduce
1. Create a functional component with `useState` hook.
2. Add a `for` loop inside the component (but outside the hook).
3. Run the ESLint with the `eslint-react-hooks` plugin enabled.

```tsx
const Component = () => {
  const [state, setState] = useState(0);

  for (let i = 0; i < 10; i++) {
    console.log(i);
  }

  return <div></div>;
};
```

### Link to code example:
https://codesandbox.io/p/devbox/8dlj6f
Run `npm run lint`

## The current behavior
ESLint throws an error about `useState` potentially being called multiple times, even though it is not in a loop.

## The expected behavior
No ESLint error should be thrown, as `useState` is not inside the loop, and should follow the rule of hooks correctly.
