# [DevTools Bug]: When I opened react-devtools on my terminal,can not see the component tree,

> Issue #31602 - Created on 11/21/2024

> Original URL: https://github.com/facebook/react/issues/31602

## Description

### Website or app

http://localhost:5173/

### Repro steps

When I opened react-devtools on my terminal,

And my project connects to localhost:8097 through "<script src="http://localhost:8097"></script>", which is the service port of react-devtools.

But I turned off the react-devtools browser extension,

The result is that although the terminal is connected to the react-devtools, but can not see the component tree,

I think it's the browser extension that injects something into the web. I don't want to use the browser extension react-devtools, Instead, view the component tree with "<script src="http://localhost:8097"></script>" and the terminal's react-devtools,

What should I do in my code

https://github.com/user-attachments/assets/2bf3dae7-10f7-4be3-9db4-9e8e77bc235d



### How often does this bug happen?

Every time

### DevTools package (automated)

6.0.1

### DevTools version (automated)

6.0.1

### Error message (automated)

can not see the component tree,

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
