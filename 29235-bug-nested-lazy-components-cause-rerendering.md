# Bug: Nested lazy components cause rerendering

> Issue #29235 - Created on 5/23/2024

> Original URL: https://github.com/facebook/react/issues/29235

## Description

This is a duplicate of https://github.com/facebook/react/issues/27573, which was closed without response. We're noticing this issue at scale, and it's fairly pronounced, with hundreds of rapid re-renders triggered by a single lazy component. I've forked the replication from original issue to demonstrate that this is still an issue in React 19:

https://codesandbox.io/p/sandbox/react-lazy-rerender-bug-forked-q4q6ym


## The current behavior

The lazy parent component renders multiple times:

<img width="181" alt="Screenshot 2024-05-23 at 10 54 06 AM" src="https://github.com/facebook/react/assets/4248263/482a32b0-d1e0-4220-a2db-33a5e0cb9254">

(In our environment, we've seen the number of re-renders proliferate to the hundreds. This matches the below reproduction.)

## The expected behavior

The lazy parent component should only render one time.

---

The original issue had a reply that included a reproduction that matched the issue we're experiencing more closely: https://codesandbox.io/p/sandbox/react-lazy-suspense-5g75x3

Similar to what we're seeing, this repro has hundreds of re-renders, and the number is nondeterministic.

<img width="105" alt="Screenshot 2024-05-23 at 11 06 11 AM" src="https://github.com/facebook/react/assets/4248263/7871459c-de6e-4880-933a-da83498d4720">

<img width="103" alt="Screenshot 2024-05-23 at 11 06 21 AM" src="https://github.com/facebook/react/assets/4248263/78525dd5-4f2e-49d2-b719-122139423830">

---

Our workaround for now is a lightweight replacement for `Suspense` using the Transition API to defer its lazy children, for usage in nested lazy contexts:

```tsx
export const DeferredSuspense: FunctionComponent<SuspenseProps> = (props) => {
  const [isDeferred, setIsDeferred] = useState(true);

  useEffect(() => {
    startTransition(() => setIsDeferred(false));
  }, []);

  if (isDeferred) {
    return props.fallback;
  }

  return <Suspense {...props} />;
};
```
