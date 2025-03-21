# [Compiler Bug]: `SyntaxError: Unexpected token, expected "{"` for components declared with arrow function and implicit returns

> Issue #31639 - Created on 11/27/2024

> Original URL: https://github.com/facebook/react/issues/31639

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhHCA7MAXABAEQFEAxAQQFUAZAFQH0BJfXAXlwHIMEAPbGAQwC0YANYBLAA4CMfAG5sAOhkXdxEGHmC4AymPEA5WZVEZhuAL64AZjAgBbdgDoA9MYAm3B3AA2ohBmwOAFZgCkqcXKrquOhYeDoSBjIAwpjYfnisABTAiri4oq4sBCQUNAz4imYAlCwAfLgAPK6iMvmuzMAFFk61IGZAA

### Repro steps

## Throw an error

```js
const DEFAULT_ID = 'nextra-skip-nav'

export { SkipNavLink } from './index.client.js'

export const SkipNavContent = ({
  id = DEFAULT_ID
}) => <div id={id} />
```

## optimized with react-compiler

```js
const DEFAULT_ID = 'nextra-skip-nav'

export { SkipNavLink } from './index.client.js'

export const SkipNavContent = ({
  id = DEFAULT_ID
}) => {
  return <div id={id} />
}
```

### How often does this bug happen?

Every time

### What version of React are you using?

playground

### What version of React Compiler are you using?

playground
