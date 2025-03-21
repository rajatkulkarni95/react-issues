# [Compiler Bug]: useMemo returns a result that contains a ref that needs to be declared as a dependency

> Issue #29587 - Created on 5/25/2024

> Original URL: https://github.com/facebook/react/issues/29587

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [X] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEUYCAsgJ4ASEEA1gBQCURwAOsUXIWDt9Ew4ASgjREAvCTKi0jAIzNOnIkRgIcsYqQoIAthEYtJAPjYrVajVvNdLRAPQOiAYV54AJgnUeiAQzB-Ii8ABwRML2xKC3seLBExABplO0snIgBVMiIIcQxsfF4iPEDMCH4eTDBPbwRfP2CEMIjwuGjU1QBzDQBJTDx8PwAbADVhqARZYw4Oy3VNGGI8fsHR8cmxADo4WHUhAG4YywBfZNTjo-SeogALP18cCCI9Pxh6AXjZf0CG0PDItpER5Ebr8AZAp48PQhPBDBDFYghIZ+SidGCCDybCynIgAbTiQlkAF0lJgLphOPlcARtGQAGIQGB6RjLAZ4YZjIYTVgzVSVPgItkc9ZfKQ6Kas1ac7kWfn8arQuGi6QbOSKFKqeY2HTkfSGYwSMy8ubWRa2eyqdJuKo1HzfIJ-FpRI6qSXstZc1VnF2OZxZeG5IhUwpVYqlcoCG1eO2-Jr-VrtC0g3ord3S1XTH2a01LVPCz2yba7cI4Q6zU4ai3qMg4BlMxhoRl6cgQLxDHlZoNNvo4PzYBCbGsNpsttukpPk+yTtLOa6YBB1CHPV7vN35iZfPu+BVI1X2x0AvAIQLLHIwaNdmDFfjAqEwuEIohIlFojHYxJ4tcejdJIg7pViCSnDkpwCAAB4hIy-BeGgfhQEM-DBjSRBUAAgiEISZlwcqXnokgqnWzLGq6HjIEQ8hnPYmB+HoCBkQA5NQCBwpg9HYqSFhamajBHAAPAARlAOCPBSsyEC4Qx4HA9ASMABpGp2jZMps1YaIRw7KV+6aFjsMB7Dg44Wsc06qCYPqiDWfEOIJwmEGZXDMGW5IgMcQA

### Repro steps

```ts
function useMyHook() {
  const countRef = useRef(1)

  return useMemo(() => {
    return {
      // Considered as a dependency
      countRef,

      // Use of functions is not considered a dependency
      getCountRef() {
        return countRef.current;
      },
    }
    // I had to mark countRef as a dependency to get it to compile in playground.
  }, [countRef])
}
```
In the code above, countRef needs to be marked as a dependency in order for the playground to compile, but ref is always stable during rendering.

**playground**: CannotPreserveMemoization: React Compiler has skipped optimizing this component because the existing manual memoization could not be preserved. The inferred dependencies did not match the manually specified dependencies, which could cause the value to change more or less frequently than expected

**local project**: skips compilation when not marked as a dependency.

### How often does this bug happen?

Every time

### What version of React are you using?

playground
