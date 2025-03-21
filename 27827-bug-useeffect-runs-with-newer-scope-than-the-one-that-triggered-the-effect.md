# Bug: useEffect runs with newer scope than the one that triggered the effect

> Issue #27827 - Created on 12/12/2023

> Original URL: https://github.com/facebook/react/issues/27827

## Description


React version: 18.2.0

## Steps To Reproduce

If this can be confirmed as a bug, I'll try to create a repo that shows the bug in action.

## The current behavior

I have this hook:
```
function useWtf(a?: string, b?: string) {
  console.log("outside effect", a, b)
  useEffect(() => {
    console.log("inside effect", a, b)
  }, [a])
}
```

When quickly changing the variables, such as in StrictMode, I manage to get this output:

```
outside effect NOT_STARTED undefined
outside effect NOT_STARTED  undefined
inside effect NOT_STARTED undefined
outside effect PENDING NOT_STARTED
outside effect PENDING PENDING
inside effect PENDING PENDING
```

The effect is triggered when `a` is changed to `PENDING`. At that moment `b` is `NOT_STARTED`. So I expected this to hold true for when the effect runs as well. But if the hook is run quickly, that is not always the case. As shown here, once the effect is run `b` has already changed to `PENDING`.

## The expected behavior

The effect should run with the scope that is available when the effect is triggered. While I can't find any documentation that specifies if this is something that `useEffect` guarantees, it feels like the most logical thing.
