# [DevTools Bug]: Console.log in second call to useMemo callback in strict mode is not dimmed or suppressed

> Issue #27989 - Created on 1/19/2024

> Original URL: https://github.com/facebook/react/issues/27989

## Description

### Website or app

https://codesandbox.io/p/devbox/tender-aryabhata-xtrckf?file=%2Fapp%2Fpage.tsx

### Repro steps

This only happens in the canary version of react. Most likely due to the changes made in #25583.

To repro:
1. Enable strict mode
2. Call console.log from inside a useMemo callback, e.g.:
```js
  useMemo(() => {
    console.log("useMemo callback")
  }, [])
```

In React 18.2.0, the log from the second strict mode call to the useMemo callback will be dimmed or suppressed (depending on devtools settings). In React 18.3.0-canary-60a927d04-20240113 (or nextjs 14.0.4), both calls are logged normally.

Note: when using codesandbox to repro, look at the logs from the browser devtools console, not the embedded one in codesandbox, which doesn't always show the same output.

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
