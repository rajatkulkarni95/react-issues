# Bug: [Strict Mode] Inconsistent behavior updating reducer state in mount Effect vs. update Effect

> Issue #30712 - Created on 8/15/2024

> Original URL: https://github.com/facebook/react/issues/30712

## Description

When rendering an app using `<StrictMode />`, calling a reducer's `dispatch` function in an Effect appears to have different observable behaviors depending on whether the Effect is mounting or updating.

React version: 18.3.1

Steps to reproduce:

1. Dispatch a reducer action in an Effect where the reducer contains internal invariants depending on the current state (see reproduction below).
2. Render the component in `<StrictMode />`.
3. When the Effect dispatches on mount, the reducer's invariants can be violated causing an error to be thrown. The same does not occur when the Effect dispatches on update.

Minimal reproduction:

In this reproduction, both components call `useReducer` with a reducer function containing invariants, e.g. to prevent invalid states. For this reproduction, the reducer toggles a boolean value to `true` once and throws an error for any future dispatches. 

Each component then calls `useReducer's` `dispatch` function in an Effect. The reducer's invariant is only violated in `<MountEffectDispatch />`, not `<UpdateEffectDispatch />` even though _both_ are being double-invoked as part of `<StrictMode />`.

This specific way of surfacing the different behaviors between mount and update Effects is simplified from an app I'm developing so it may obfuscate the underlying issue (if there is one). 

This behavior isn't seen outside of `<StrictMode />`.

```tsx
function MountEffectDispatch() {
  const [value, dispatch] = useReducer((prevValue) => {
    if (prevValue) {
      throw new Error("Already true");
    }

    return !prevValue;
  }, false);

  useEffect(() => {
    dispatch();
  }, []);

  return <p>{String(value)}</p>;
}

function UpdateEffectDispatch() {
  const [value, dispatch] = useReducer((prevValue) => {
    if (prevValue) {
      throw new Error("Already true");
    }

    return !prevValue;
  }, false);

  // Will be used to defer dispatching to a later render
  const [mounted, setMounted] = useState(false);

  useEffect(() => {
    setMounted(true);
  }, []);

  useEffect(() => {
    if (!mounted) {
      return;
    }

    dispatch();
  }, [mounted]);

  return <p>{String(value)}</p>;
}


ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <UpdateEffectDispatch /> // or <MountEffectDispatch />
  </React.StrictMode>
);
```

## The current behavior

Reducer state updates in mount Effects behave differently from reducer state updates in update Effects when using `<StrictMode />`.

## The expected behavior

Reducer state updates should behave consistently in any Effect when using `<StrictMode />`.

