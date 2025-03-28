# Consider changing the next property type of the update object of the dispatchSetState function from any to null

> Issue #30081 - Created on 6/25/2024

> Original URL: https://github.com/facebook/react/issues/30081

## Description

Hi! 

It's not bug, but I think there is an unnecessary any type.
The type of the next property has changed since [this commit](https://github.com/facebook/react/commit/b617db3d966f678eb0b4aac6d96f7967b37a9e91).
I think the any type might be unstable. Considering future changes.

React version: 18.2.0

## Steps To Reproduce

1. Change the type of Update. (type  Update<S, A> in ReactFiberHooks)
2. Check for null in next where it is used.

Link to code example:

before
```ts
const update: Update<S, A> = {
  lane,
  revertLane: NoLane,
  action,
  hasEagerState: false,
  eagerState: null,
  next: (null: any),
};
```

after
```ts
export type Update<S, A> = {
  lane: Lane,
  revertLane: Lane,
  action: A,
  hasEagerState: boolean,
  eagerState: S | null,
  next: Update<S, A> | null,
};

const update: Update<S, A> = {
  lane,
  revertLane: NoLane,
  action,
  hasEagerState: false,
  eagerState: null,
  next: null,
};
```

## The current behavior
When adding a function, the wrong type may be entered.

## The expected behavior
Can improve type stability
