# Bug: When I use useNavigate hook in my project, it got error for not good use of hook ,But I use hook as tutorial

> Issue #31257 - Created on 10/15/2024

> Original URL: https://github.com/facebook/react/issues/31257

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1.
const router = createBrowserRouter([{
  path: '/', element: LogIn()
}, { path: 'hall', element: Hall() }])

const root = ReactDOM.createRoot(
  document.getElementById('root') as HTMLElement
);
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <RouterProvider router={router}></RouterProvider>
    </Provider>
  </React.StrictMode>
);


2.
import React from "react";
import { useNavigate } from "react-router-dom";
function Hall() {
    const navi = useNavigate()
    function handle() {
        navi('/hall')
    }
    return(
         <div>  
            <Button>
            OK
        </Button></div>
    )
}
export default Hall;

there is only one react version that is 18.3.1
<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
window is blank , and got error on colsole;

index.tsx:9 Warning: Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons:
1. You might have mismatching versions of React and the renderer (such as React DOM)
2. You might be breaking the Rules of Hooks
3. You might have more than one copy of React in the same app
See https://reactjs.org/link/invalid-hook-call for tips about how to debug and fix this problem.
printWarning @ react.development.js:209
error @ react.development.js:183
resolveDispatcher @ react.development.js:1592
useContext @ react.development.js:1602
useNavigate @ index.js:195
Hall @ index.tsx:9
./src/index.tsx @ index.tsx:15
__webpack_require__ @ bootstrap:22
(anonymous) @ startup:6
(anonymous) @ startup:6
Show 5 more frames
Show less
react.development.js:1618 Uncaught TypeError: Cannot read properties of null (reading 'useContext')
    at Object.useContext (react.development.js:1618:1)
    at useNavigate (index.js:195:7)
    at Hall (index.tsx:9:1)
    at ./src/index.tsx (index.tsx:15:10)
    at __webpack_require__ (bootstrap:22:1)
    at startup:6:1
    at startup:6:1



## The expected behavior

no error and page redered 

