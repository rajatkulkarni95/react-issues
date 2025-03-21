# Bug: Poor error message when useEffect is called with no parameters

> Issue #32354 - Created on 2/11/2025

> Original URL: https://github.com/facebook/react/issues/32354

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0.0

## Steps To Reproduce

1. Call `useEffect()` - note the lack of arguments


Link to code example:

* https://codesandbox.io/p/sandbox/pqx384
* https://github.com/JoshuaKGoldberg/repros/tree/react-use-effect-no-arguments

## The current behavior

```plaintext
Uncaught TypeError: create is not a function
    at react-stack-bottom-frame (react-dom-client.development.js:22509:20)
    at runWithFiberInDEV (react-dom-client.development.js:543:16)
    at commitHookEffectListMount (react-dom-client.development.js:10758:29)
    at commitHookPassiveMountEffects (react-dom-client.development.js:10878:11)
    at reconnectPassiveEffects (react-dom-client.development.js:12802:11)
    at recursivelyTraverseReconnectPassiveEffects (react-dom-client.development.js:12774:9)
    at reconnectPassiveEffects (react-dom-client.development.js:12849:11)
    at doubleInvokeEffectsOnFiber (react-dom-client.development.js:15696:13)
    at runWithFiberInDEV (react-dom-client.development.js:543:16)
    at recursivelyTraverseAndDoubleInvokeEffectsInDEV (react-dom-client.development.js:15656:17)
    at commitDoubleInvokeEffectsInDEV (react-dom-client.development.js:15705:7)
    at flushPassiveEffects (react-dom-client.development.js:15470:13)
    at eval (react-dom-client.development.js:15324:11)
    at MessagePort.performWorkUntilDeadline (scheduler.development.js:44:48)
```

## The expected behavior

Ideally not crash - or crash with a better error message?

In #15197 the reviews seemed to pointed towards a dev-only warning, rather than an invariant.

---

Re-opening of #15194 because the stalebot closed it.
