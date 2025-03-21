# [DevTools Bug] Cannot add node "20" because a node with that id is already in the Store.

> Issue #27902 - Created on 1/9/2024

> Original URL: https://github.com/facebook/react/issues/27902

## Description

### Website or app

http://127.0.0.1:8081/

### Repro steps

Uncaught Error: Cannot add node "20" because a node with that id is already in the Store.
The error was thrown at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1128815
    at C.emit (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1099142)
    at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1100830
    at bridgeListener (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1501170)

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.0.0-993c4d003

### Error message (automated)

Cannot add node "20" because a node with that id is already in the Store.

### Error call stack (automated)

```text
at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1128815
    at C.emit (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1099142)
    at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1100830
    at bridgeListener (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1501170)
```


### Error component stack (automated)

_No response_

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot add node  because a node with that id is already in the Store. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

