# [DevTools Bug] Cannot remove node "434" because no matching node was found in the Store.

> Issue #27780 - Created on 12/3/2023

> Original URL: https://github.com/facebook/react/issues/27780

## Description

### Website or app

localhost

### Repro steps

1.log to admin panel
2.go to user info

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

4.28.5-ef8a840bd

### Error message (automated)

Cannot remove node "434" because no matching node was found in the Store.

### Error call stack (automated)

```text
at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1126778
    at A.emit (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1095954)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1097642
    at bridgeListener (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1495532)
```


### Error component stack (automated)

_No response_

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot remove node  because no matching node was found in the Store. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

