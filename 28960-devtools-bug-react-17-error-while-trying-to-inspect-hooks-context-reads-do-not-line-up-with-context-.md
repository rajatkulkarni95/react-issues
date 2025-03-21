# [DevTools Bug]: React 17 error while trying to inspect hooks "Context reads do not line up with context dependencies."

> Issue #28960 - Created on 5/1/2024

> Original URL: https://github.com/facebook/react/issues/28960

## Description

### Website or app

https://github.com/gdeedlerthryv/react-dev-tools-test/

### Repro steps

1. Inspect TestApp component
2. Get error 

```
backendManager.js:117 React DevTools encountered an error while trying to inspect hooks. This is most likely caused by an error in current inspected component: "TestApp".
The error thrown in the component is: 

 Error: Context reads do not line up with context dependencies. This is a bug in React Debug Tools.
    at H (react-debug-tools.production.min.js:14:310)
    at Proxy.useContext (react-debug-tools.production.min.js:18:40)
    at Object.useContext (chunk-GGTEBMAR.js?v=b51a6ac3:1125:29)
    at useLocation (chunk-PFB6EJD6.js?v=b51a6ac3:3382:16)
    at TestApp (main.jsx:13:20)
    at R (react-debug-tools.production.min.js:32:287)
    at exports.inspectHooksOfFiber (react-debug-tools.production.min.js:35:150)
    at inspectElementRaw (renderer.js:3379:36)
    at Object.inspectElement (renderer.js:3716:38)
    at agent.js:420:18
```

![Screenshot 2024-04-30 at 3 58 07 PM](https://github.com/facebook/react/assets/122398572/f06b54da-5eda-417d-bc78-a0bfacef8fcc)


Issue was introduced by DevTools 5.1.0 release, I think [this PR is the culprit.](https://github.com/facebook/react/pull/28467) I built the 5.0.2 extension and the error did not occur:
![Screenshot 2024-04-30 at 3 57 37 PM](https://github.com/facebook/react/assets/122398572/6c8fc9ef-f3d5-429e-b2a2-8e1e4d4fd320)

I wasn't able to repro the issue without external libraries, but someone who knows better probably could.

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
