# [React 19] Fiber is missing a debug information

> Issue #29092 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29092

## Description

## Summary

In **React 18**, Fiber exposed `_debugSource`

<img width="210" alt="updateQueue null" src="https://github.com/facebook/react/assets/18378585/0d989b4c-0993-4e49-883b-039b1f0c81ba">

In **React 19** (19.0.0-rc-915b914b3a-20240515) this was changed to `_debugInfo` but the value is alway `null`

<img width="203" alt="updateQueue null" src="https://github.com/facebook/react/assets/18378585/e74bdf29-cea2-49fd-b00a-755eb92bc495">

