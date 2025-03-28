# Bug: Ensure createRoot warning parity with ReactDOM.render

> Issue #32175 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32175

## Description

Ensure createRoot warning parity with ReactDOM.render

### Description

This PR addresses an internal task to bring over some pre-existing warnings for `ReactDOM.render()` to `createRoot()`, ensuring parity in warning behavior. Specifically, warnings related to failing to clear an existing React tree should now also trigger for roots.

### Steps to Reproduce

1. Use `ReactDOM.render()` with a non-empty container.
2. Use `createRoot()` with a non-empty container.
3. Observe that warnings for `ReactDOM.render()` appear, but not for `createRoot()`.

### Expected Behavior

Warnings for failing to clear the React tree should trigger for both `ReactDOM.render()` and `createRoot()`.

### Actual Behavior

Warnings appear only for `ReactDOM.render()` and not for `createRoot()`.

### Environment

- React Version: 16.13.0
- Browser: Chrome
- Node Version: 12.18.0

