# [React 19] infinite loop when using React lazy & functional formAction together.

> Issue #29930 - Created on 6/19/2024

> Original URL: https://github.com/facebook/react/issues/29930

## Description

## Summary

### Version
"react": "19.0.0-rc-107a2f8c3e-20240617",
"react-dom": "19.0.0-rc-107a2f8c3e-20240617"
OS : windows 11
Chrome : 125.0.6422.142

### Overview
We have a great feature 'functional form action' in react 19.
`<form action={functionalFormAction}`
<br>

but with React lazy, it doesn't seem to work properly.
It causes infinite loop depends on its use cases.

![image](https://github.com/facebook/react/assets/17701725/bd5e67a6-e990-45b8-a57a-531e81617863)

<br>

1. case1 : infinite loop (React lazy without `<Suspense/>`. All dynamic codes are inside form component)
2. case2 : no infinite loop (React lazy with `<Suspense/>`. All dynamic codes are inside form component)
3. case3 : infinite loop (React lazy with `<Suspsne />` & has dependency on useFormStatus. All dynamic code are inside form component)

### Related Issues
#29235 Bug: Nested lazy components cause rerendering
#27573 Bug: Nested components imported with React.lazy cause rerendering

### Reproduction
Go to [CodeSandBox](https://codesandbox.io/p/devbox/devbox-test-hhr-zm6z3k?file=%2Fsrc%2FApp.tsx%3A11%2C46)
Try Case2 at first, (submit form by clicking button)
Try Case3 at second, (it causes infinite loop so it makes js blocked)
Try Case1 at the last (it causes infinite loop so it makes js blocked)


### Preview
App.tsx
![image](https://github.com/facebook/react/assets/17701725/1300ae79-1c3c-4f79-bd82-06e723ed6b9f)

Case1.tsx
![image](https://github.com/facebook/react/assets/17701725/761d08d4-8fd7-4692-b0a8-954f1124df48)



Case 1 Result
![image](https://github.com/facebook/react/assets/17701725/f18f610c-7b4b-42fe-88b9-4bd8addc5d86)


Case 2 Result
![image](https://github.com/facebook/react/assets/17701725/17b3eba5-ae81-4017-83de-bb3a17e5b4e3)


Case 3 Result
![image](https://github.com/facebook/react/assets/17701725/4eac93e2-e498-483c-9a8c-7bc99c2b20b9)


