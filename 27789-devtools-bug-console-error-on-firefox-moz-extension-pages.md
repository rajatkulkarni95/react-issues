# [DevTools Bug]: Console error on Firefox "moz-extension:*" pages 

> Issue #27789 - Created on 12/5/2023

> Original URL: https://github.com/facebook/react/issues/27789

## Description

### Website or app

Every page of almost any extension opened as window in Firefox

### Repro steps

1. Install the React Dev Tools in Firefox.
2. Open the Console tab in the Dev Inspector.
3. On Urls like moz-extension://da25b98a.... (any extension link) a console error appears.

`The extension "React Developer Tools" is not allowed to access moz-extension://da25b98a-****-****-****-********0940/popup/popup.html`

For think it would be ok, if the React Dev Tools are inaccessible on moz-extension:* pages.

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
