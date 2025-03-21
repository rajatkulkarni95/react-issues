# [React 19] Conditionally rendered suspendable component using `use()` shows fallback even if promise already resolved

> Issue #30701 - Created on 8/15/2024

> Original URL: https://github.com/facebook/react/issues/30701

## Description

## Summary
I'm trying the new `use()` hook over promises. I found that the suspense will show the fallback if the call to `use()` is delayed, even if the promise already resolved prior to `use`ing it. Namely, Suspense always renders the fallback initially, even if the component never suspends. 

Interestingly, if I `use` the promise in a sibling component, this issue is not present even on the first suspense component.

## Reproduction
[Here's a minimal reproducible example](https://github.com/mordechaim/lazy-suspense).

<details>
<summary>Code backup</summary>

```ts

import { Suspense, use, useMemo, useState } from 'react';

export function App() {
  const [open, setOpen] = useState(false);

  const promise = useMemo(
    () =>
      new Promise<string>((resolve) => {
        console.log('starting promise');

        setTimeout(() => {
          console.log('resolving promise');

          resolve('hello');
        }, 5000);
      }),
    []
  );

  return (
    <>
      <div>
        <button onClick={() => setOpen(true)}>Reveal</button>
        {open && (
          <Suspense fallback='still loading...'>
            <SuspendableGreeting promise={promise} />
          </Suspense>
        )}
      </div>

      {/* Uncommenting the below code will fixed the issue above */}
      {/* <Suspense fallback='loading'>
        <Resolve promise={promise} />
      </Suspense> */}
    </>
  );
}

interface SuspendableProps {
  promise: Promise<string>;
}

function SuspendableGreeting({ promise }: SuspendableProps) {
  const greeting = use(promise);
  return greeting;
}

function Resolve({ promise }: SuspendableProps) {
  use(promise);
  return null;
}
```
</details>



1. Run `npm run dev`
2. Open the page and DevTools
3. Wait 5 seconds for the message "resolving promise" to print
4. Press "Reveal"



