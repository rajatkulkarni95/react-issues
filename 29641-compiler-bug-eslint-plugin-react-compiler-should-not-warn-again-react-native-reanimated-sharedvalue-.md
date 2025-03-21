# [Compiler Bug]: eslint-plugin-react-compiler should not warn again react-native-reanimated sharedValue mutation

> Issue #29641 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29641

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/software-mansion/react-native-reanimated/

### Repro steps

## Contexte

react-native-reanimated is an animation librairie largely used by react-native dev.
This library allow to use [`sharedValue`](https://docs.swmansion.com/react-native-reanimated/docs/fundamentals/glossary#shared-value) that we can mutate to update UI animation

## Issue

With this library, it is expected that you mutate `sharedValue` returned by `useSharedValue` hook.
But `eslint-plugin-react-compiler` throw **"Mutating a value returned from a function whose return value should not be mutatedeslint(react-compiler/react-compiler)"** error

Exemple

```ts
import { NativeScrollEvent } from 'react-native';
import { useAnimatedScrollHandler, useSharedValue } from 'react-native-reanimated';

export const useList = () => {
  const someScrollSharedValue = useSharedValue(0);

  const onScroll = useAnimatedScrollHandler({
    onScroll: (event: NativeScrollEvent) => {
      /**
       * Here we have eslint issue:
       * Mutating a value returned from a function whose return value should not be mutatedeslint(react-compiler/react-compiler)
       */
      someScrollSharedValue.value = event.contentOffset.y;
    },
  });

  return { onScroll };
};
``` 

## Question

How can you solve this issue, is this a library issue & do `react-native-reanimated` have to do some declaration work to tell `react-compiler` that it's safe to mutate value ?
Or can we configure somehow our project to tell ?

### How often does this bug happen?

Often

### What version of React are you using?

18.2.0
