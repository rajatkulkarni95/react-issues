# [Feature Request] Warn for arrays resulting of `.map()` or `.filter()` in hook dependencies

> Issue #31538 - Created on 11/14/2024

> Original URL: https://github.com/facebook/react/issues/31538

## Description

ESLint plugin react hooks version: 4.6.0

## Steps To Reproduce

```tsx
const MyComponent = () => {
  const array = useMemo(() => ["banana", "apple"], []);

  const filteredArray = array.filter((element) => element !== "apple");

  useEffect(() => {
    console.log("If this is printed, array has changed");
  }, [array]);

  useEffect(() => {
    console.log("If this is printed, filteredArray has changed");
  }, [filteredArray]);

  const [counter, setCounter] = useState(0);

  return <button onClick={() => setCounter(counter + 1)}>Re-render</button>;
};
```

## Feature request
The exhaustive-deps rule already warns for functions declared in the scope of a component, which will be re-declared at each render and thus be a problem if put inside the dependency array of a `useEffect`, `useCallback` or `useMemo`. I recently had a problem when applying the `.filter()` method on a memoized array, since the new resulting array is a new one at each render.

I was wondering if it would be possible to warn for this kind of issues as well, the same way functions declared inside the component are currently warned.

I don't have an exhaustive list of such methods (that return a new object from a given one) that would be warned, other than `.filter()` and `.map()`, perhaps people in the comments can propose others?

## Where to do this
I have dived a little bit in the code of the package and found the `scanForConstructions` function ([here](https://github.com/facebook/react/blob/380f5d675d2269f090d15c3f92e10de66e12516c/packages/eslint-plugin-react-hooks/src/ExhaustiveDeps.js#L1584)) that seems to be the one that checks for the functions. If this is the way to do it, I could try to implement this other behaviour in this same function.

