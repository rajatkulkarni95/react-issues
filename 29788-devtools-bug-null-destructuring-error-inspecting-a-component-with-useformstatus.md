# [DevTools Bug]: Null destructuring error inspecting a component with `useFormStatus`

> Issue #29788 - Created on 6/7/2024

> Original URL: https://github.com/facebook/react/issues/29788

## Description

### Website or app

https://github.com/markerikson/react-19-rdt-useformstatus-error

### Repro steps

1. Clone https://github.com/markerikson/react-19-rdt-useformstatus-error
2. Install and run with `yarn && yarn dev`
3. Browse to http://localhost:5173/useformstatus-example
4. Open up the React DevTools Extension and inspect the `<SubmitButton>` component
5. Observe that the inspection fails with `Cannot destructure property 'pending' of 'useFormStatus(...)' as it is null.`

![image](https://github.com/facebook/react/assets/1128784/8ad7105b-8944-4717-a6ee-fa015e4f6b67)

/cc @hoxyq @eps1lon 

FWIW I ran across this while working on updating Replay.io's own support for React 19 by merging down all the last year's worth of changes to our long-running RDT fork:

- https://github.com/replayio/react/pull/14

and then I was inspecting this `<SubmitButton>` component in a Replay recording of the example app, and observed that I see this error when inspecting it in the recording:

- Open https://app.replay.io/recording/e2e-example-rdt-react-19distindexhtml--edab8c19-e2a2-4269-bb37-948cd5dff465?commentId=&focusWindow=eyJiZWdpbiI6eyJwb2ludCI6IjAiLCJ0aW1lIjowfSwiZW5kIjp7InBvaW50IjoiMjUzMTI0NDcxODc5NjU0NDMzMTY0NzMzNTcxNTA0NTM3NjAiLCJ0aW1lIjoxMjc1MX19&point=13629779253886577472836196156573656&primaryPanel=debugger&secondaryPanel=react-components&time=6926&viewMode=dev
- Try inspecting `<SubmitButton>` and see that we report "can't inspect the component"

I do note that in the `getPrimitiveStackCache()` function in `react-debug-tools`, we don't try to warm up `Dispatcher.useFormStatus()`.  Tried adding that myself and rebuilding our RDT fork bundle, but it didn't seem to fix the behavior, so that may not be relevant.

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
