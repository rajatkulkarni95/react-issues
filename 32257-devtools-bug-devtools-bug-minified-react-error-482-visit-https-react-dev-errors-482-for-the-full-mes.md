# [DevTools Bug]:  [DevTools Bug] Minified React error #482; visit https://react.dev/errors/482 for the full message or use the non-minified dev environment for full errors and additional helpful warnings.

> Issue #32257 - Created on 1/29/2025

> Original URL: https://github.com/facebook/react/issues/32257

## Description

### Website or app

website 

### Repro steps

trying to catch the component using react dev tools

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

6.1.0-b000019578

### Error message (automated)

Minified React error #482; visit https://react.dev/errors/482 for the full message or use the non-minified dev environment for full errors and additional helpful warnings.

### Error call stack (automated)

```text
at trackUsedThenable (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:45359)
    at useThenable (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:49037)
    at Object.use (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:49258)
    at t.use (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:240881)
    at ActualSourceButton (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1389072)
    at renderWithHooks (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:47208)
    at updateFunctionComponent (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:84514)
    at beginWork (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:98436)
    at performUnitOfWork (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:167733)
    at workLoopSync (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:167590)
```

### Error component stack (automated)

```text
at ActualSourceButton (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1388949)
    at Suspense (<anonymous>)
    at Components_InspectedElementViewSourceButton (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1389400)
    at div (<anonymous>)
    at div (<anonymous>)
    at InspectedElementWrapper (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1389911)
    at InspectedElementContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1347917)
    at va (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1334647)
    at div (<anonymous>)
    at InspectedElementErrorBoundaryWrapper (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1340957)
    at NativeStyleContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1373326)
    at div (<anonymous>)
    at div (<anonymous>)
    at OwnersListContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1287112)
    at SettingsModalContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1316397)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1412929
    at va (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1334647)
    at div (<anonymous>)
    at div (<anonymous>)
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1337358)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1337555
    at div (<anonymous>)
    at div (<anonymous>)
    at div (<anonymous>)
    at ThemeProvider (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1337358)
    at TimelineContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1414942)
    at ProfilerContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1406733)
    at TreeContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1228907)
    at SettingsContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1256772)
    at ModalDialogContextController (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1394425)
    at DevTools_DevTools (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1563309)
```

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Minified React error #482; visit https://react.dev/errors/482 for the full message or use the non-minified dev environment for full errors and additional helpful warnings. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```
