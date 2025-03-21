
### How can I force update a class component in SyncLane? Can we permanently expose runWithPriority API?

> Issue #28897 - Created on 4/24/2024

> Original URL: <https://github.com/facebook/react/issues/28897>

## Description

In react 18 concurrency, sometime we want to specify a higher priority for UI update triggered by external store.

This can be done for function component by using `useSyncExternalStore`.

However, I can't find any information on how to make class component's forceUpdate to be in SyncLane.

In react experimental version, I can use unstable_runWithPriority API to achieve this. Is there a more stable way to do it?