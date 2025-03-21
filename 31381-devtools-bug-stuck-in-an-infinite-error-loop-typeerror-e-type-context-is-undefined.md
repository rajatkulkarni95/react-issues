# [DevTools Bug]: Stuck in an infinite error loop: TypeError: e.type._context is undefined

> Issue #31381 - Created on 10/29/2024

> Original URL: https://github.com/facebook/react/issues/31381

## Description

### Website or app

https://github.com/leerob/next-saas-starter

### Repro steps

When using Firefox with the latest version of React DevTools installed, loading any page on a Next.js 15 and React 19 app triggers an infinite loop with the following error:

`TypeError: e.type._context is undefined`

![image](https://github.com/user-attachments/assets/e0abf70e-4c69-4872-aa89-b43c01003f43)

![image](https://github.com/user-attachments/assets/42c28ee2-da7d-40d2-9a5b-42b945435077)

I added an example repo as the reproduction repo because the issue is consistent across all Next.js 15 + React 19 apps.

This issue does not occur in Chrome. Additionally, if I disable React DevTools, the errors stop appearing.




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
