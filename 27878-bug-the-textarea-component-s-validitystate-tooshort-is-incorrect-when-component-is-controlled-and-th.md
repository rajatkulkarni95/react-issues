# Bug: the <textarea> component's ValidityState.tooShort is incorrect when component is controlled and the value is passed in via the value prop

> Issue #27878 - Created on 1/5/2024

> Original URL: https://github.com/facebook/react/issues/27878

## Description

React version: 18.2.0

## Steps To Reproduce

1. Create a controlled `<textarea>` component with the value passed to the *value* prop (not as children)
2. Pass a *minLength* prop with a value > 0

Link to code example: https://codesandbox.io/p/sandbox/react-textarea-bug-mjwyw5

## The current behavior
If the `<textarea>` component is part of a form, submission of the form occurs even if the length of the value in the `<textarea>` is less than the value passed in to the *minLength* prop and no invalid event is fired. Checking the `<textarea>` element's ValidityState shows that the element is valid and `ValidityState.tooShort` is `false`.

## The expected behavior
Submission of the form should be prevented and an invalid event should fire. The ValidityState of the element should show `ValidityState.tooShort` as `true`.
