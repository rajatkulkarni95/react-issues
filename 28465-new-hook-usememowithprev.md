# New hook: useMemoWithPrev

> Issue #28465 - Created on 2/28/2024

> Original URL: https://github.com/facebook/react/issues/28465

## Description

Sometimes you may need access to previous/last value of useMemo hook. Something similar is available when we set state (useState hook).

Some use case would be:

```
// current useMemo
const memoValueWithUseMemo = useMemo(() => {
  const shouldGetReevaluated = someExpensiveOperation(dep1, dep2, dep3);
  const otherStuff1 = getOtherStuff1(dep1);
  const otherStuff2 = getOtherStuff2(dep2);
  const otherStuffN = getOtherStuffN(dep3);

  return { shouldGetReevaluated, otherStuff1, otherStuff2, otherStuffN };
}, [dep1, dep2, dep3]);

```

I am suggesting something like this:

```
const memoValueWithUseMemoWithPrev = useMemoWithPrev(
  (prev) => () => {
    // additional prev value is available
    // evade expensive operation
    if (prev.shouldGetReevaluated) {
      return prev;
    }
    const shouldGetReevaluated = someExpensiveOperation(dep1, dep2, dep3);

    const otherStuff1 = getOtherStuff1(dep1);
    const otherStuff2 = getOtherStuff2(dep2);
    const otherStuffN = getOtherStuffN(dep3);

    return { shouldGetReevaluated, otherStuff1, otherStuff2, otherStuffN };
  },
  [dep1, dep2, dep3],
);

```

The hook itself would be something like this:

```

const useMemoWithPrev = (calculateValueFunction, dependencies) => {
    const prev = useRef({});

    const memoValue = useMemo(calculateValueFunction(prev.current), dependencies || []);
    prev.current = memoValue;
    return memoValue;
  };

```

Difference is that we would need to pass function that returns function, but that's it.
It probably couldn't be done by updating current useMemo because useMemo can be used to memoize higher order functions, so difference in callback we pass to it cannot determine whether we want to use it with previous value or not.

If we have this we could skip even more calculations than we are already skipping with useMemo.

Yes, this can be done by adding the same thing to our code, but it would be cool to have this in react.

