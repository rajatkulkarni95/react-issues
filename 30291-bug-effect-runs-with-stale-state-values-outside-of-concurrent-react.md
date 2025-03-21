# Bug: effect runs with stale state values outside of Concurrent React

> Issue #30291 - Created on 7/8/2024

> Original URL: https://github.com/facebook/react/issues/30291

## Description

```tsx
const [done, setDone] = useState(false);
useEffect(() => {
  if (done) return;
  setDone(true);
  console.log("🤔 This runs more than once.");
});
```

I have held an assumption that a React effect will only run once the state change queue has been processed. In other words, a new run of a useEffect would only be kicked off once the state values are settled. This does not seem to be the case in the examples below.

I understand that Concurrent React might throw a wrench in this model, but the examples below run on React 18.3, and no concurrent features are used. In particular, I can’t identify any low or high priority changes in the examples.

I understand that state change batching exists. But I expected for the batching to finish before running effects.

I fully admit, that it is likely my mental model of React here is wrong. However, if the effects are not guaranteed to run before the state changes are settled, then does that mean that we can not reason about the state of state values in effects at all and should be ready for anything? It seems too weak of a guarantee for common use, which is why I am hesitant to accept it as the simplest explanation.

Regardless, any response will be highly appreciated!

React version: 18.3.1

## Steps To Reproduce

1. Open [the minimal reproduction](https://codesandbox.io/s/effect-stale-state-4zzwns?file=/src/App.js).
    <details><summary>Code backup</summary>
      
        import { useEffect, useState } from "react";
     
        export default function () {
          const [done, setDone] = useState(false);
          useEffect(() => {
            if (done) return;
            setDone(true);
            console.log("%cMust run once", "color:red");
          });
        
          return <></>;
        }
    </details>
2. Open the console.
3. Actual behavior: “Must run once” is logged twice.
4. Expected behavior: “Must run once” is logged once.

### Note on the initial rerender
The minimal reproduction relies on the setup running the effect an extra time to begin with. I don’t understand why it does that, but it enables the demo. We can side-step and have a slightly longer demo that does not rely on the initial extra render:

1. Open [the larger reproduction](https://codesandbox.io/s/effect-stale-state-multiple-542q4q?file=/src/App.js).
    <details><summary>Code backup</summary>
        import { useEffect, useReducer, useState } from "react";
        
        let fastRendersRemaining = 0;
        
        export default function () {
          const [rerenderId, rerender] = useReducer((i) => i + 1, 0);
        
          useEffect(() => {
            if (fastRendersRemaining === 0) return;
            fastRendersRemaining -= 1;
            queueMicrotask(rerender);
          });
        
          const [done, setDone] = useState(true);
          useEffect(() => {
            // console.log('Current values:', { rerenderId, done });
            if (done) return;
            setDone(true);
            console.log("%cMust run once", "color:red");
          });
        
          return (
            <button
              onClick={() => {
                fastRendersRemaining = 5;
                rerender();
                setDone(false);
              }}
            >
              Run demonstration
            </button>
          );
        }

    </details>
2. Open the console.
3. Click on “Run demonstration”.
4. Actual behavior: “Must run once” is logged six times.
5. Expected behavior: “Must run once” is logged once.

