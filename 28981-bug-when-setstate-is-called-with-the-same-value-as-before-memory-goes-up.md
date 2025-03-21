# Bug: When setState is called with the same value as before, memory goes up

> Issue #28981 - Created on 5/3/2024

> Original URL: https://github.com/facebook/react/issues/28981

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

The issue seems to be, when I change a state variable with `setState`, and if I do `setState(x)` and `x` is the same as the current state variable inside a `useInterval` hook, the memory starts to grow. I'm using `usehooks-ts` but I also tried with other hooks (Dan Abramov's hook and Josh Comeau's hook)

This is the code causing the issue:
```ts
  const [charge, setCharge] = useState<number>(0);

  function updateRemainingCharge() {
    setCharge((prev) => {
      const sameValue = maybeTrue(0.99999);
      return sameValue ? prev : prev + 1;
    });
  }

  useInterval(updateRemainingCharge, 5);

  const [charge, setCharge] = useState<number>(0);
```

But if I do:
```ts
  const maybeTrue = (odds: number) => Math.random() < odds;
  const toSym = (num: number) => Symbol(num);
  const fromSym = (sym: Symbol) => Number(sym.description);
  
  const [charge, setCharge] = useState<Symbol>(Symbol(0));

  function updateRemainingCharge() {
    setCharge((prev) => {
      const sameValue = maybeTrue(0.99999);
      const num = fromSym(prev);
      return sameValue ? toSym(num) : toSym(num + 1);
    });
  }

  useInterval(updateRemainingCharge, 5);
```

it doesn't leak. I'm aware I can fix it by stopping the interval, but that seems like an optimization and in my original code the delay was slow, so there was not even a need for immediate optimization.

React version: 18.2.66

## Steps To Reproduce

1. Go to https://ovp-two.vercel.app/
2. on chrome start to track memory, check the memory going up while the number doesn't change

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: 
https://github.com/arturcarvalho/op

Link to deployed code: https://ovp-two.vercel.app/

I don't know how to debug memory leaks on codesandbox, it seems to hide them.


<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Memory goes up when `setState(x)` where `x` is the same as current `x` on state variable.

## The expected behavior
Memory **not** go up when `setState(x)` where `x` is the same as current `x` on state variable.

