# Bug: React Context API Not Updating Correctly with Concurrent Mode

> Issue #27806 - Created on 12/7/2023

> Original URL: https://github.com/facebook/react/issues/27806

## Description

### Bug Description

I've encountered an issue where the React Context API does not seem to update correctly when used in conjunction with React's Concurrent Mode. The context value appears to become "stuck" at its initial value, failing to update when the provider's value changes.

### Steps to Reproduce

1. Enable Concurrent Mode in a React application.
2. Create a Context with a dynamic value managed by a state hook.
3. Consume the context in a component and update the state.
4. Observe that the context does not update in the consuming component.

### Expected Behavior

The expected behavior is for the consuming component to re-render with the new context value when the provider's state changes.

### Actual Behavior

The context value in the consuming component does not update after the initial render, even though the provider's state has changed.

### Reproducible Demo

[Link to a CodeSandbox or GitHub repo with a minimal reproducible demo of the issue.]

### Environment

- React Version: 17.0.2
- Browser: Chrome 91.0.4472.124
- OS: macOS Big Sur 11.4

### Additional Context

This issue seems to be related specifically to Concurrent Mode, as disabling Concurrent Mode resolves the problem. It's critical for the correct functioning of context-dependent features in our application.

Thank you for looking into this issue.

