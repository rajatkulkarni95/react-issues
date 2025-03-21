# [DevTools Bug]: Hook parsing fails if a hook uses useSyncExternalStore

> Issue #27889 - Created on 1/7/2024

> Original URL: https://github.com/facebook/react/issues/27889

## Description

### Website or app

https://react-devtools-issue-demo.vercel.app/

### Repro steps


1. Open up this page: https://react-devtools-issue-demo.vercel.app/ (source: https://github.com/jamesbvaughan/react-devtools-issue-demo/blob/main/src/App.tsx)
2. Open up the React dev tools
3. Navigate to the Components tab
5. Observe in the right sidebar that hook name parsing fails for one of the two components.

---

Hook name parsing is _really_ helpful when debugging/optimizing large components with lots of hooks, and this issue makes that feature unusable on components whose hooks make use of `useSyncExternalStore`.

This is particularly painful for my current work, where nearly all components make use of [Zustand](https://github.com/pmndrs/zustand) stores, which use `useSyncExternalStore` internally.

---

This is the same symptom that folks are hitting in https://github.com/facebook/react/issues/24980, but I'm not sure whether the cause is the same for everyone there.

### How often does this bug happen?

Every time

### DevTools package (automated)

_No response_

### DevTools version (automated)

_No response_

### Error message (automated)

_No response_

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
