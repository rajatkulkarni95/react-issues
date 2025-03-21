# [DevTools Bug] Cannot read properties of undefined (reading 'concat')

> Issue #27908 - Created on 1/9/2024

> Original URL: https://github.com/facebook/react/issues/27908

## Description

### Website or app

on a localy hosted react app (v18.2.0)

### Repro steps

after recording a profil in the profiler panel, I clicked on the graph in the top-right corner.

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.0.0-993c4d003

### Error message (automated)

Cannot read properties of undefined (reading 'concat')

### Error call stack (automated)

```text
at updateTree (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1114468)
    at getCommitTree (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1113282)
    at rr.getCommitTree (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1116473)
    at CommitFlamegraphAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1353046)
    at Lf (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:40670)
    at Gh (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:61725)
    at Yn (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:118951)
    at Rk (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:103877)
    at Qk (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:103805)
    at df (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:103623)
```


### Error component stack (automated)

```text
at CommitFlamegraphAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1352847)
    at div
    at div
    at div
    at SettingsModalContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1253868)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1484419
    at bo (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1271707)
    at div
    at div
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1274418)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1274615
    at div
    at div
    at div
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1274418)
    at TimelineContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1344475)
    at ProfilerContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1336084)
    at TreeContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1166113)
    at SettingsContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1194207)
    at ModalDialogContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1278876)
    at DevTools_DevTools (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1492154)
```


### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot read properties of undefined (reading 'concat') in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

