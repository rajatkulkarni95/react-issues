# Bug: Error "Unsupported URL scheme" with React Developer Tools

> Issue #29636 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29636

## Description

When using React Developer Tools in Chrome, I encounter an error message "Unsupported URL scheme; Fallback: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME". This error occurs when I try to debug my React application.

React version: 18.3.1
React Developer Tools version: 5.2.0

Steps to reproduce:

1. Open a React application in Chrome.
2. Open React Developer Tools.
3. Try to debug the application.

Expected result:
I should be able to debug my application without encountering any errors.

Actual result:
I encounter the error "Unsupported URL scheme; Fallback: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME".

Error message:
```
Unsupported URL scheme; Fallback: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME
```

Additional information:
I have tried the following steps to resolve the issue, but none of them worked:

Restarting the browser.
Reinstalling React Developer Tools.
Updating the browser.

Here is a snippet from my code:
**Code snippet:**
```javascript
if (typeof window !== 'undefined') {
  window.global = window;
}

import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

const root = createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);


