# [Compiler Bug]: [ESLINT][React Native] Animated and ref.current error: Ref values (the `current` property) may not be accessed during render.

> Issue #31643 - Created on 11/28/2024

> Original URL: https://github.com/facebook/react/issues/31643

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

...

### Repro steps

```tsx
import React, { useRef } from 'react';
import { Animated } from 'react-native';

export function Test() {
  const valueRef = useRef(new Animated.Value(0));
  const animatedStyle = { opacity: valueRef.current };
  //                               ^^^
  // ESLint: Ref values (the `current` property) may not be accessed during render. (https://react.dev/reference/react/useRef)(react-compiler/react-compiler)
  return <Animated.View style={animatedStyle} />;
}

```

### How often does this bug happen?

Every time

### What version of React are you using?

latest

### What version of React Compiler are you using?

0.0.0-experimental-df7b47d-20241124
