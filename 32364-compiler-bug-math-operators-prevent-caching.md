# [Compiler Bug]: math operators prevent caching

> Issue #32364 - Created on 2/12/2025

> Original URL: https://github.com/facebook/react/issues/32364

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAYjHgpgCYAyeYOAFMEWuZVWEQL4CURwADrEiAGwQ4iADyIBeIgikAHSmDwA3BIzYVqYXgG5hRaQGpTRkTAmxijYyaIAeKhoB8DxwKndPzgPSu6h4ihsLcINxAA

### Repro steps

```ts
  let x = expensive(friends);
  x++;
```
It's not memoized, and `expensive` is called on every render.


---


https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAYjHgpgCYAyeYOAFMEWuZVWADREQ4AWCGEQC+ASiLAAOsSIAbBDiIAPIgF4iCZQAdKYPADcEjNhWpgxAbhlEieNEUZ9BMCdNm3lAai-XZImyIYRVhiRkDbAB4qQwA+CNtJZQCPIkiAehiDeNkrGREQESA
 

```ts
  let x = expensive(friends);
  if (other) {
    x++;
  }
```
Similar. Not cached.

---


https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAYjHgpgCYAyeYOAFMEWuZVWADREQ4AWCGEQC+ASiLAAOsSIAbBDiIAPIgF4iCZQAdKYPADcEjNhWpgxAbhlEieNEUZ9BMCdNm3VGgIw3RfmEVYYkY-WwAeKkMAPjDbSWUROPCAeiiDWNkrGREQESA
```ts
  let x = expensive(friends);
  if (other) {
    x = 1
  }
```
Cached properly.

### How often does this bug happen?

Every time

### What version of React are you using?

latest from playground

### What version of React Compiler are you using?

latest from playground
