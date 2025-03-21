# [DevTools Bug]: React instrumentation encountered an error: TypeError: e.hasOwnProperty is not a function.

> Issue #27851 - Created on 12/20/2023

> Original URL: https://github.com/facebook/react/issues/27851

## Description

### Website or app

https://github.com/molnard1/react-template/tree/devtools-bug

### Repro steps

1. Clone the above repo (the `devtools-bug` branch should be used), install dependencies (`npm i`)
2. Build/start it in **development** mode (`npm run watch`)
3. Observe the following error in console, along with devtools not working:
![image](https://github.com/facebook/react/assets/101341428/c90e9b13-9ff0-41d7-854c-9c7038c7c5e2)
![image](https://github.com/facebook/react/assets/101341428/96c2ca50-2929-4e4b-ae5b-d3fe5dc36b7e)

As far as I can tell, this appears to be caused by Axios, as this error does not happen before adding it to the project.

### How often does this bug happen?

Every time

### DevTools package (automated)

_No response_

### DevTools version (automated)

_No response_

### Error message (automated)

_No response_

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
