# [Compiler]: InvalidReact: Hooks must be the same function on every render, but this value may change over time to a different function

> Issue #31591 - Created on 11/20/2024

> Original URL: https://github.com/facebook/react/issues/31591

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhHCA7MAXABFMBARSgRgE9cBeXACgH0AHAQ2wAtlccYBLDAcwCU1AHy5gAX1wB6abgDMMACa4WMbJQA2PAEYAdDAfRY8zRj2riDuG7n4JstFu2Tc+Qqxlu2YD2F+Brb1sAMwc4DjphKjEw7AinVjZBABoZOQwIGABbZk1cOIig4PxCEjJyTlposQJiUgpE9mFZBWVVZnUtXWLg2TqAWShsVh5MKprxCV6bacMvWzm5gwQAD0YsvCUEEOYoTTwQqAw4bDGvAfIAQUZGas8bYxxcJVZmSzMeADp7RwByaRsBCaTQQP6CL51cqNQRBXzYfy4AA8Sh4ADcRAAJYGg3AAdSymiUSOkqIxAG4DHMQBIgA

### Repro steps

Hello,

I have installed and setup `eslint-plugin-react-compiler`.

Given the following code:
```tsx
import api from `@shared/api`
export default function JobsPage() {
  const { data, status, refetch } = api.get("/hello").useQuery()
                                 // ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ - `Hooks must be the same function on every render, but this value may change over time to a different function`
}
```
 `eslint-plugin-react-compiler` will report the error `Hooks must be the same function on every render` 
The error is correct, but I still don't see anything really wrong with that code. 

Can you please take a look and see if this case here is a false positive? 
Should this code be treated as OK?
If not, do you have a suggestion of what could be done as an alternative?


#### What version of `eslint-plugin-react-compiler` are you using?

`19.0.0-beta-0dec889-20241115`

### How often does this bug happen?

Every time

### What version of React are you using?

18.2.0

### What version of React Compiler are you using?

/
