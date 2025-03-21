# [DevTools Bug] Could not find node with id "155" in commit tree

> Issue #27832 - Created on 12/13/2023

> Original URL: https://github.com/facebook/react/issues/27832

## Description

### Website or app

Chrome

### Repro steps

I was working on a development task. After logging in to an internal website, I click "Inspect" to open the developer tool in Chrome and select profiler. 
Next, I clicked "start profiling" and refresh the page. After everything is rendered, I stopped profiling. When reading the profile data by clicking the component and the time it was rendered, this exception was thrown from time to time. I tried to refresh the frame but this didn't help at all.

### How often does this bug happen?

Often

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.0.0-993c4d003

### Error message (automated)

Could not find node with id "155" in commit tree

### Error call stack (automated)

```text
at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1118876
    at Map.forEach (<anonymous>)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1118825
    at rr.getRankedChartData (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1119305)
    at CommitRankedAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1355868)
    at Lf (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:40670)
    at Gh (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:61725)
    at Yn (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:118951)
    at Rk (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:103877)
    at Qk (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:103805)
```


### Error component stack (automated)

```text
at CommitRankedAutoSizer (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1355625)
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
https://api.github.com/search/issues?q=Could not find node with id  in commit tree in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```
<img width="817" alt="Screenshot 2023-12-12 at 3 18 08 PM" src="https://github.com/facebook/react/assets/44010473/7782901b-6f73-4409-bea0-a5597a4815dc">

