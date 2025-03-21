# Bug: Fix suspense replaying forward refs

> Issue #32218 - Created on 1/25/2025

> Original URL: https://github.com/facebook/react/issues/32218

## Description

The Component is not a function error is thrown when using Suspense and forwardRef together in a specific way.

It seems like react-reconciler doesn't properly handle forwardRefs in either renderWithHooksAgain, replaySuspendedComponentWithHooks, replayFunctionComponent or replaySuspendedUnitOfWork. The Component variable is not a function in this case, but a { $$typeof: Symbol(react.forward_ref), render: (props, ref) => any }. renderWithHooksAgain tries to execute Component(props, secondArg), which throws this error.


React version:
18.3.0-next-3ba7add60-20221201
## Steps To Reproduce

1. occur when Suspending components rerender in a specific order.



## Expected Behavior
- Components using `forwardRef` wrapped in `Suspense` should render correctly without errors during the replay of suspended units of work.
- The `replaySuspendedUnitOfWork` function should correctly identify and handle `forwardRef` components by invoking their `render` method.

## Current Behavior
- When a `forwardRef` component is wrapped with `Suspense` and a suspension occurs, React throws a "Component is not a function" error during the replay phase.
- The `replaySuspendedUnitOfWork` function attempts to invoke the `type` property directly, which is not appropriate for `forwardRef` components, leading to the error.


