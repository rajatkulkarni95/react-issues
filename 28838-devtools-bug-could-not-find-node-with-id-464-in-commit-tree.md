# [DevTools Bug] Could not find node with id "464" in commit tree

> Issue #28838 - Created on 4/15/2024

> Original URL: https://github.com/facebook/react/issues/28838

## Description

### Website or app

https://github.com/rafeulanamudoy/TourShare-FrontEnd

### Repro steps

debugging my nextjs project to find out which component is slowing down my application by using react devtools profiler section. when i start recording by clcking the blue button it start recording. then when  go to my page and navigate different page like first i sign in to my application  and then navigate from home  to my dashboard.and when i stop the recording this error occured.

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.0.2-47cf347e4

### Error message (automated)

Could not find node with id "464" in commit tree

### Error call stack (automated)

```text
at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1121414
    at Map.forEach (<anonymous>)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1121363
    at qe.getRankedChartData (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1121843)
    at CommitRankedAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1363588)
    at Sf (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:40362)
    at Qh (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:62110)
    at Vn (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:119822)
    at fl (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:104666)
    at el (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:104594)
```


### Error component stack (automated)

```text
at CommitRankedAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1363345)
    at div
    at div
    at div
    at SettingsModalContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1255750)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1492330
    at Co (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1273325)
    at div
    at div
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1276036)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1276233
    at div
    at div
    at div
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1276036)
    at TimelineContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1352197)
    at ProfilerContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1343811)
    at TreeContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1168008)
    at SettingsContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1196102)
    at ModalDialogContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1280512)
    at DevTools_DevTools (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1500065)
```


### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Could not find node with id  in commit tree in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

