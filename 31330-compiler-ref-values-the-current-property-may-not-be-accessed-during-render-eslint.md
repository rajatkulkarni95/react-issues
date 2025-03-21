# [Compiler]: Ref values (the `current` property) may not be accessed during render. (eslint)

> Issue #31330 - Created on 10/23/2024

> Original URL: https://github.com/facebook/react/issues/31330

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

no

### Repro steps

```tsx
import { useEffect, useRef } from 'react'

type TOptional<T> = T | undefined

export function usePrevious<T>(value: T): TOptional<T> {
  const ref = useRef<TOptional<T>>()
  useEffect(() => {
    ref.current = value
  }, [value])
  return ref.current // error here.. 
}

```

What's wrong with this usePrevious hook ? 

### How often does this bug happen?

Every time

### What version of React are you using?

19 beta

### What version of React Compiler are you using?

beta
