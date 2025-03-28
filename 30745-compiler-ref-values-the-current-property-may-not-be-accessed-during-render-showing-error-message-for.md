# [Compiler]: Ref values (the `current` property) may not be accessed during render - showing error message for custom hooks

> Issue #30745 - Created on 8/19/2024

> Original URL: https://github.com/facebook/react/issues/30745

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/gkiely/react-eslint-vite

### Repro steps
```sh
git clone https://github.com/gkiely/react-eslint-vite
npm i 
npm run lint
```

Each of these show an error message:
- Pass a ref to a custom hook
- Set ref.current inside a useCallback and pass to a custom hook
- useImperativeHandle

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-6ebfd5b0-20240818
