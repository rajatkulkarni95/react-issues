# Bug: startTransition gets stuck on infinite Suspense

> Issue #29126 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29126

## Description

I'm building a mobile web app with tabs and stack navigation, so I need Offscreen or React Freeze (https://github.com/software-mansion/react-freeze, simulates Offscreen using Suspense). If I also use `startTransition`, the updates within `startTransition` never get rendered.

React version: 18.3.1

## Steps To Reproduce

1. Have a component that suspends indefinitely (e.g. frozen using React Freeze)
2. `setState` inside `startTransition`

Link to code example: https://codesandbox.io/p/sandbox/blazing-wood-nmw92p

## The current behavior
React waits for the frozen component to unsuspend before completing the transition.

## The expected behavior
React ignores the frozen component and completes the transition as if the frozen component wasn't there.

## Additional info
I don't want transitions to wait for suspended components, I'm just using `startTransition` for time slicing. I know it was intentional to make transitions wait for suspended components to avoid showing too many spinners, but not everyone wants that, I think there should be a way to enable time slicing without opting in to this feature. I think before, I could've done something like `useTransition({ timeoutMs: 0 })`, which should've allowed me to complete the transition while ignoring suspense.

With React 18, is there a way to either:
1. make `startTransition` not wait for the suspended component OR
2. enable time slicing without `startTransition`
