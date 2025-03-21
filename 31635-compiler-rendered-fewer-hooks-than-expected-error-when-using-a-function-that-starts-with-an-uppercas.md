# [compiler] "Rendered fewer hooks than expected" error when using a function that starts with an uppercase character

> Issue #31635 - Created on 11/26/2024

> Original URL: https://github.com/facebook/react/issues/31635

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhASwLYAcIwC4AEwBUYCAyngIZ4IEC+BAZjBBgQOQwJVx4cAdAHaYc+AgCUefACIB5ALLNW7LtLwBaACZsA9HAA2aBEP7DhcCELCEpWVgQC8BABQBKJwD4iwggUvWhADaAPoANARkeJQ0CAC6TiRkMbQueDBQCG6+BNx4sEKuOX4APJ7FfgQlAEZQeHhWBFYAwkZwANaOwO5ekQjR1KnVvQCE1W70ngpU7XQYdHAwVGAAFiW6tfVW5YWVpViewM0raAZazWw4QiZ47vTrBxXrO37ZQvTmQgE2BMen55crDdEj1HN5gDk8gUqp5AImE-ja7QIeBWdE2DSEz2EHyEwikvDw8gUADpFjxaBIIBBbjo4FB5qZiQBzfoAUQMCAZeAAQgBPACSWhcXCp-DcbmJ3CEWgQMBcJTsDl0njeIHoQA

### Repro steps

The application crashes when clicking the button. The the local state of `Repro` changes so it re-rendereds and that's when the error is triggered.

- If the `ChildComponent` function is renamed to `childComponent`, the issue disappears.
- If the `ChildComponent` function is refactored to an arrow function with implicit return, the issue disappears: `const ChildComponent = () => <>↑ click the button</>`
- When rendering the child component as usual (`<ChildComponent />` the error is not triggered). I know that should be the normal thing to do, but I had this problem because a third party library was expecting children components being of a specific types. I started doing regular components and when I noticed that limitation I changed them to function calls and that's when I found this problem in the react compiler.

This issue doesn't happen when the application is built without the `babel-plugin-react-compiler` plugin.


https://github.com/user-attachments/assets/84bda515-7280-48b1-a679-971d58cc6840





### How often does this bug happen?

Every time

### What version of React are you using?

18.3.1

### What version of React Compiler are you using?

19.0.0-beta-0dec889-20241115
