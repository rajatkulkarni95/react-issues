# [React 19] When multiple components call `use` inside a `Suspense`, it crosses the boundary of `Suspense` and stops rendering of other `Suspense` as well

> Issue #29905 - Created on 6/15/2024

> Original URL: https://github.com/facebook/react/issues/29905

## Description

## Summary

```tsx
import { Suspense, use, useState } from "react";

const f = async (wait) => {
  await new Promise((resolve) => setTimeout(resolve, wait));
  return new Date();
};

const App = () => {
  const [open, setOpen] = useState(false);

  return (
    <>
      <Expected />
      <Unexpected />
    </>
  );
};

const Expected = () => {
  const [open, setOpen] = useState(false);

  return (
    <>
      <div>👍</div>
      <button onClick={() => setOpen(!open)}>{open ? "close" : "open"}</button>
      {open && <List wait={[1000, 2000, 3000, 4000, 5000]} />}
    </>
  );
};

const Unexpected = () => {
  const [open, setOpen] = useState(false);

  return (
    <>
      <div>🤔</div>
      <button onClick={() => setOpen(!open)}>{open ? "close" : "open"}</button>
      {open && <List wait={[1000, 2000, 3000, 3000, 5000]} />}
    </>
  );
};

const List = ({ wait }) => {
  const [t1] = useState(f(wait[0]));
  const [t2] = useState(f(wait[1]));
  const [t3] = useState(f(wait[2]));
  const [t4] = useState(f(wait[3]));
  const [t5] = useState(f(wait[4]));

  return (
    <>
      <Suspense fallback={<div>Loading No.1 ...</div>}>
        <Item time={t1} />
      </Suspense>
      <Suspense fallback={<div>Loading No.2 ...</div>}>
        <Item time={t2} />
      </Suspense>
      <Suspense fallback={<div>Loading No.3 ...</div>}>
        <Item time={t3} />
      </Suspense>
      <Suspense fallback={<div>Loading No.4 & No.5 ...</div>}>
        <Item time={t4} />
        <Item time={t5} />
      </Suspense>
    </>
  );
};

const Item = ({ time }) => {
  const t = use(time);

  console.log("render item");

  return <div>{t.toISOString()}</div>;
};

export default App;

```
https://codesandbox.io/p/sandbox/use-and-suspense-hlcjk6

The two components `<Expected>`👍 and `<Unexpected>`🤔 are expected to behave in the same way. That is, No.1 to No.3 should be displayed one second apart, and No.4 and No.5 should be displayed two seconds after No.3 is displayed.

There is a difference in the waiting time for No.4 between `<Expected>` and `<Unexpected>`, being 4 seconds or 3 seconds, but since they are wrapped together in `<Suspense>` with No.5, they should be throttled and displayed after 5 seconds.

However, in `<Unexpected>`, not only that, but No.3, which should belong to a different `<Suspense>` scope, is also displayed after 5 seconds. This seems to break the behavior of `<Suspense>`.

---

Please note that this is a different issue from the one being discussed in https://github.com/facebook/react/pull/26380. I am issuing a Promise outside of Suspense and passing it as props.

