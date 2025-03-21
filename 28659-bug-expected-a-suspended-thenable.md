# Bug:  Expected a suspended thenable.

> Issue #28659 - Created on 3/27/2024

> Original URL: https://github.com/facebook/react/issues/28659

## Description

I was working in a NextJS app router (in a React Server Component), and I get this error:
```
 ⨯ Error: Expected a suspended thenable. This is a bug in React. Please file an issue.
    at stringify (<anonymous>)
 ⨯ Error: Expected a suspended thenable. This is a bug in React. Please file an issue.
    at stringify (<anonymous>)
digest: "1072417316"
```
In the browser console I see:
```
helpers.js:113 Uncaught TypeError: Cannot read properties of undefined (reading 'call')
    at options.factory (webpack.js?v=1711459236570:731:31)
    at __webpack_require__ (webpack.js?v=1711459236570:37:33)
    at fn (webpack.js?v=1711459236570:386:21)
    at requireModule (react-server-dom-webpack-client.browser.development.js:156:23)
    at initializeModuleChunk (react-server-dom-webpack-client.browser.development.js:1357:1)
    at readChunk (react-server-dom-webpack-client.browser.development.js:1167:1)
    at mountLazyComponent (react-dom.development.js:16652:1)
    at beginWork$1 (react-dom.development.js:18388:1)
    at beginWork (react-dom.development.js:26791:1)
    at performUnitOfWork (react-dom.development.js:25637:1)
    at workLoopConcurrent (react-dom.development.js:25623:1)
    at renderRootConcurrent (react-dom.development.js:25579:1)
    at performConcurrentWorkOnRoot (react-dom.development.js:24432:1)
    at workLoop (scheduler.development.js:256:1)
    at flushWork (scheduler.development.js:225:1)
    at MessagePort.performWorkUntilDeadline (scheduler.development.js:534:1)

The above error occurred in the <NotFoundErrorBoundary> component:

    at NotFoundErrorBoundary (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/not-found-boundary.js:76:9)
    at NotFoundBoundary (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/not-found-boundary.js:84:11)
    at DevRootNotFoundBoundary (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/dev-root-not-found-boundary.js:33:11)
    at ReactDevOverlay (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/react-dev-overlay/internal/ReactDevOverlay.js:84:9)
    at HotReload (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/react-dev-overlay/hot-reloader-client.js:307:11)
    at Router (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/app-router.js:182:11)
    at ErrorBoundaryHandler (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/error-boundary.js:115:9)
    at ErrorBoundary (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/error-boundary.js:162:11)
    at AppRouter (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/components/app-router.js:542:13)
    at ServerRoot (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/app-index.js:129:11)
    at RSCComponent
    at Root (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/client/app-index.js:145:11)

React will try to recreate this component tree from scratch using the error boundary you provided, ReactDevOverlay.
window.console.error @ app-index.js:33
console.error @ hydration-error-info.js:45
eval @ console.js:36
logCapturedError @ react-dom.development.js:15128
callback @ react-dom.development.js:15190
callCallback @ react-dom.development.js:8206
commitCallbacks @ react-dom.development.js:8253
commitClassCallbacks @ react-dom.development.js:21256
commitLayoutEffectOnFiber @ react-dom.development.js:21358
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21351
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21340
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21510
recursivelyTraverseLayoutEffects @ react-dom.development.js:22860
commitLayoutEffectOnFiber @ react-dom.development.js:21370
commitLayoutEffects @ react-dom.development.js:22846
commitRootImpl @ react-dom.development.js:26104
commitRoot @ react-dom.development.js:25957
commitRootWhenReady @ react-dom.development.js:24677
finishConcurrentRender @ react-dom.development.js:24642
performConcurrentWorkOnRoot @ react-dom.development.js:24487
workLoop @ scheduler.development.js:256
flushWork @ scheduler.development.js:225
performWorkUntilDeadline @ scheduler.development.js:534
```

React version: 18.2.0
NextJS version: 14.1.4

## Steps To Reproduce

1. Visit homepage
2. Get this error

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
I get an error I cannot recover from

## The expected behavior
No error
