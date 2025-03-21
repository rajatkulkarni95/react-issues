# [DevTools Bug] getCommitTree(): Invalid commit "2" for root "1". There are only "1" commits.  

> Issue #30661 - Created on 8/12/2024

> Original URL: https://github.com/facebook/react/issues/30661

## Description

### Website or app

development website

### Repro steps

Uncaught Error: getCommitTree(): Invalid commit "1" for root "1". There are only "1" commits.


### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.3.1-ccb20cb88b

### Error message (automated)

getCommitTree(): Invalid commit "2" for root "1". There are only "1" commits.

### Error call stack (automated)

```text
at getCommitTree (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1156298)
    at fe.getCommitTree (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1159973)
    at CommitRankedAutoSizer (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1405976)
    at renderWithHooks (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:52335)
    at updateFunctionComponent (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:79640)
    at beginWork (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:93314)
    at performUnitOfWork (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:150703)
    at workLoopSync (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:150571)
    at renderRootSync (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:150302)
    at recoverFromConcurrentError (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:146135)
```


### Error component stack (automated)

```text
at CommitRankedAutoSizer (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1405777)
    at div
    at div
    at div
    at SettingsModalContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1297185)
    at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1534843
    at ua (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1314716)
    at div
    at div
    at ThemeProvider (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1317427)
    at chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1317624
    at div
    at div
    at div
    at ThemeProvider (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1317427)
    at TimelineContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1394187)
    at ProfilerContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1385842)
    at TreeContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1209165)
    at SettingsContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1237405)
    at ModalDialogContextController (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1321890)
    at DevTools_DevTools (chrome-extension://gpphkfbcpidddadnkolkpfckpihlkkil/build/main.js:1:1542579)
```


### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=getCommitTree(): Invalid commit  for root . There are only  commits. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

