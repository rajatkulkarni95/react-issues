# [DevTools Bug] Cannot add node "1" because a node with that id is already in the Store.

> Issue #29904 - Created on 6/15/2024

> Original URL: https://github.com/facebook/react/issues/29904

## Description

### Website or app

localhost://3000

### Repro steps

inspect page

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.1.0-b566064da

### Error message (automated)

Cannot add node "1" because a node with that id is already in the Store.

### Error call stack (automated)

```text
emit@moz-extension://93cf03db-73dc-4729-802f-cbdecaa028ae/build/main.js:1:1091557
A/this._wallUnlisten<@moz-extension://93cf03db-73dc-4729-802f-cbdecaa028ae/build/main.js:1:1093245
bridgeListener@moz-extension://93cf03db-73dc-4729-802f-cbdecaa028ae/build/main.js:1:1498935
```


### Error component stack (automated)

_No response_

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot add node  because a node with that id is already in the Store. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

