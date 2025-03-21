# Feature: Release ReactCurrentDispatcher as a consumable API to be used in conjunction with useExternalSyncStore

> Issue #27812 - Created on 12/8/2023

> Original URL: https://github.com/facebook/react/issues/27812

## Description

Hey folks, based on the request I obviously don't want to get fired lol. However I have fallen in love with the useExternalSyncStore hook as it has enabled me to move away from using mobx as an external state manager that is able to update react components.

Now I can have react components that don't need to be wrapped in a observer function or need classes that have observables properties referenced once on the class and another time within the constructor...

However one thing I loved about mobx is its seem less way of telling when the observable was in a react component or somewhere else and would still return the same value or update your state if in a react component with an elaborate uses symbols.

I want to do the same with thing here where I either return  `() => useExternalSyncStore(_subscribe, () => currentState[property])` or just `() => currentState[property]`. But the only discernible way of doing this is if I can detect if the property is being called in a react component. 

Here is where ReactCurrentDispatcher comes into play, after digging around the source code and I noticed that the `resolveDispatcher()` function does a check before any react hook is called in a function to see if it is within the context of reacts render phase validating if the hook has been called within the react component or not. It uses ReactCurrentDispatcher.current as a reference to see if the registered hooks are available for this component in that phase. 

I would like to use ReactCurrentDispatcher to evaluate if I should return useExternalSyncStore or just the plain version of the property that is not a part of the render cycle but needs to be referenced some place else?

Would love to hear some feedback on this as useExternalSyncStore gives us a more open source approach to handling react state externally but still doing it the react way? Even if it is not ReactCurrentDispatcher directly, just something for us to work out that we are in a react component or not?

Example:

```
  let syncedReact = { ...currentState }

  const handler = {
    get(target, property) {
      target[property] = {
        sync: () => useSyncExternalStore(_subscribe, () => currentState[property]),
        default: () => currentState[property],
      }
      let dispatcher = ReactCurrentDispatcher.current

      if (dispatcher === null) {
        return target[property].default
      }
      return target[property].sync
    },
  }

  syncedReact = new Proxy(syncedReact, handler)
```

