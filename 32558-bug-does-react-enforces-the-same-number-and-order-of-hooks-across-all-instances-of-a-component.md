# Bug: Does React enforces the same number and order of hooks across all instances of a component?

> Issue #32558 - Created on 3/9/2025

> Original URL: https://github.com/facebook/react/issues/32558

## Description

Suppose I have two instances of the same component. One uses a custom hook with two useState calls, and another uses a different custom hook with three useState calls. Intuitively, since they're separate instances, their state should be independent.

I came up with a sample implementation which works fine having different number of hooks for 2 different instances of the same component (MyComponent). This is achieved via conditionally plugging a custom hook to the component body when mounting with the help of a useState init function that guarantees picking a custom hook occurs only one time.

`const [conditionalHook] = useState(() => (count % 2 === 1) ? useCustomB : useCustomA);`

Is there any drawbacks?

**Note:** The following logic can also be used to set custom hook conditionally without a useState init function

`const conditionalHook = (count % 2 === 1) ? useCustomB : useCustomA;`

_But this is highly error prone as number and order of hooks can change even for a single component instance as prop values are modified_

Please refer to the working sample implementation below

[https://codesandbox.io/p/sandbox/stupefied-easley-yj8r9z](https://codesandbox.io/p/sandbox/stupefied-easley-yj8r9z)

Please see the following React dev tools output for these 2 instances

![Image](https://github.com/user-attachments/assets/dbbaa405-3211-46a6-9601-21ef493861f3)

![Image](https://github.com/user-attachments/assets/efc3db52-6194-4b58-980d-77bb63069ef7)

I really appreciate any clarification on this
