# [React 19] useTransition()'s pending state does not go back to false (revision 94eed63c49-20240425)

> Issue #28923 - Created on 4/26/2024

> Original URL: https://github.com/facebook/react/issues/28923

## Description

## Summary

I am excited to start using React v19 as it has so many features and QoL improvements I've been waiting for!

There is a bug (new bug comparing to v18.2.0) that I found while reproducing https://github.com/facebook/react/issues/26814. When using `useTransition()` with `use()`, `pending` flag of transition correctly becomes `true` in the beginning, but doesn't go back to `false` after transition is complete, which means any pending state artifacts in the UI remain visible.

Repository for reproducing: https://github.com/alexeyraspopov/react-beta-bugs.

Basic code (since the repo contains more than just this bug):

```ts
function SimpleAsyncFlow() {
  // this state holds instance of a promise that resolves after a second
  // the same `delayed()` function is used to trigger state update inside SimpleControlledDisplay
  let [value, setValue] = useState(() => delayed(Math.random()));
  return (
    <Suspense fallback={<p>Loading</p>}>
      <SimpleControlledDisplay promise={value} onChange={setValue} />
    </Suspense>
  );
}

function SimpleControlledDisplay({
  promise,
  onChange,
}: {
  promise: Promise<number>;
  onChange: (value: Promise<number>) => void;
}) {
  let value = use(promise);
  let [pending, startTransition] = useTransition();
  let click = () => {
    // this will trigger state update in the parent with the new 1 second promise 
    // that suppose to suspend this component, so transition should prevent it
    startTransition(() => {
      onChange(delayed(Math.random()));
    });
  };
  return (
    <div>
      <button onClick={click}>Refresh</button>
      {/* as UI "pending" state I update text style to become half transparent */}
      <p style={{ opacity: pending ? 0.5 : 1 }}>{value}</p>
    </div>
  );
}

function delayed<T>(value: T) {
  return new Promise<T>((resolve) => setTimeout(resolve, 1000, value));
}
```

Additionally here's the video reproduction, using the code from the repo I mentioned:

https://github.com/facebook/react/assets/858295/47fc5678-6c99-48f7-a55d-8b48b9bcee35


