# [DevTools Bug] Cannot read properties of undefined (reading 'replace')

> Issue #32057 - Created on 1/13/2025

> Original URL: https://github.com/facebook/react/issues/32057

## Description

### Website or app

N/A

### Repro steps

No sandbox appplies because, this error ocurrs, when I create a new app from scratch, attach flipper to that app running in IOS Simulator anda that's it. Also, Filpper App tilt in Mac Book Pro M4 Pro. 2024

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-inline

### DevTools version (automated)

4.28.0-9b95b131b

### Error message (automated)

Cannot read properties of undefined (reading 'replace')

### Error call stack (automated)

```text
at formatSourceForDisplay (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31612:35)
    at Source (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31644:14)
    at ci (http://localhost:52342/bundle.js:380:66423)
    at ll (http://localhost:52342/bundle.js:380:123310)
    at kl (http://localhost:52342/bundle.js:380:118004)
    at jl (http://localhost:52342/bundle.js:380:117935)
    at Zk (http://localhost:52342/bundle.js:380:117794)
    at cl (http://localhost:52342/bundle.js:380:114101)
    at Xk (http://localhost:52342/bundle.js:380:113074)
    at J (http://localhost:52342/bundle.js:392:1587)
```

### Error component stack (automated)

```text
at Source (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31626:11)
    at div
    at InspectedElementView_InspectedElementView (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31476:11)
    at div
    at InspectedElementWrapper (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31695:61)
    at InspectedElementContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:29899:11)
    at Suspense
    at ErrorBoundary (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28536:13)
    at div
    at InspectedElementErrorBoundaryWrapper (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28906:11)
    at NativeStyleContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:31091:11)
    at div
    at div
    at OwnersListContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:25769:11)
    at SettingsModalContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:27448:11)
    at Components_Components (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:32736:79)
    at ErrorBoundary (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28536:13)
    at PortaledContent (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28688:13)
    at div
    at div
    at div
    at ThemeProvider (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28671:11)
    at TimelineContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:32887:11)
    at ProfilerContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:32439:11)
    at TreeContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:23323:11)
    at SettingsContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:24169:11)
    at ModalDialogContextController (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:28948:11)
    at DevTools_DevTools (file:///Applications/Flipper.app/Contents/Resources/server/static/defaultPlugins/flipper-plugin-react-devtools/dist/bundle.js:41283:19)
```

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot read properties of undefined (reading 'replace') in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```
