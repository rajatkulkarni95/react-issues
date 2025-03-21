# [Compiler Bug]: Issue with React Hook Form library

> Issue #29174 - Created on 5/20/2024

> Original URL: https://github.com/facebook/react/issues/29174

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/Maxou44/issue-react-compiler-react-hook-form

### Repro steps

1. Clone `https://github.com/Maxou44/issue-react-compiler-react-hook-form`
2. Run `npm i --force && npm run start`
3. Open a web browser on `http://localhost:5173/`
4. Type something in the input field, the watched value is not displayed on the page, it's cached by the compiler

To disable the React compiler and confirm it works without the compiler, comment the line `plugins: [["babel-plugin-react-compiler", ReactCompilerConfig]],` in vite.config.mjs, relaunch `npm start` and type something in the input field

### How often does this bug happen?

Every time

### What version of React are you using?

19
