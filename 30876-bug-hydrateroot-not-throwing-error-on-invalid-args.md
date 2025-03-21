# Bug: HydrateRoot not throwing Error on invalid Args.

> Issue #30876 - Created on 9/4/2024

> Original URL: https://github.com/facebook/react/issues/30876

## Description

while working with the `hydrateRoot` call i forgot to pass the React Element (<App/>)  that shall be passed for it to work, 

like below

```
const root = hydrateRoot(container, /* this takes a  react element /* {
  onRecoverableError: (error, errorInfo) => {
    if (error.message !== "Expected error") {
      logError(error, errorInfo.componentStack);
    }
  },
});

root.render();
```


React version:

## Steps To Reproduce

Check this codesanbox [URL](https://codesandbox.io/p/sandbox/upbeat-hellman-zddp32?layout=%257B%2522sidebarPanel%2522%253A%2522EXPLORER%2522%252C%2522rootPanelGroup%2522%253A%257B%2522direction%2522%253A%2522horizontal%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522id%2522%253A%2522ROOT_LAYOUT%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522cm0mjhmea00063b6idn6hqjm3%2522%252C%2522sizes%2522%253A%255B100%255D%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522EDITOR%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522id%2522%253A%2522cm0mjhmea00023b6i2f26jg8l%2522%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522SHELLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522id%2522%253A%2522cm0mjhmea00033b6idvtxgz17%2522%257D%255D%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522DEVTOOLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522id%2522%253A%2522cm0mjhmea00053b6i7m0sa78t%2522%257D%255D%257D%255D%252C%2522sizes%2522%253A%255B50%252C50%255D%257D%252C%2522tabbedPanels%2522%253A%257B%2522cm0mjhmea00023b6i2f26jg8l%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0mjhme900013b6iw20lmua8%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522filepath%2522%253A%2522%252Fsrc%252Findex.js%2522%252C%2522state%2522%253A%2522IDLE%2522%252C%2522initialSelections%2522%253A%255B%257B%2522startLineNumber%2522%253A9%252C%2522startColumn%2522%253A14%252C%2522endLineNumber%2522%253A9%252C%2522endColumn%2522%253A14%257D%255D%257D%255D%252C%2522id%2522%253A%2522cm0mjhmea00023b6i2f26jg8l%2522%252C%2522activeTabId%2522%253A%2522cm0mjhme900013b6iw20lmua8%2522%257D%252C%2522cm0mjhmea00053b6i7m0sa78t%2522%253A%257B%2522id%2522%253A%2522cm0mjhmea00053b6i7m0sa78t%2522%252C%2522activeTabId%2522%253A%2522cm0nzfa34001f3b6ilsgx6f50%2522%252C%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0mjhmea00043b6iz2cixpbe%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%257D%252C%257B%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%252C%2522id%2522%253A%2522cm0mjhreo00133b6i1os2mhsa%2522%252C%2522mode%2522%253A%2522permanent%2522%257D%252C%257B%2522type%2522%253A%2522SANDBOX_INFO%2522%252C%2522isCloud%2522%253Afalse%252C%2522id%2522%253A%2522cm0nzfa34001f3b6ilsgx6f50%2522%252C%2522mode%2522%253A%2522permanent%2522%257D%255D%257D%252C%2522cm0mjhmea00033b6idvtxgz17%2522%253A%257B%2522tabs%2522%253A%255B%255D%252C%2522id%2522%253A%2522cm0mjhmea00033b6idvtxgz17%2522%257D%257D%252C%2522showDevtools%2522%253Atrue%252C%2522showShells%2522%253Afalse%252C%2522showSidebar%2522%253Atrue%252C%2522sidebarPanelSize%2522%253A15%257D)

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

we get to see this error 

![Screenshot 2024-09-04 at 8 04 08 PM](https://github.com/user-attachments/assets/f36be6fc-08cc-4710-81b1-a200e15661c1)

## The expected behavior

if i try to uncomment the `root.render()` call, we see that the actual error is now being shown

https://github.com/user-attachments/assets/274ac730-7b93-4948-8a06-a828c4b93cf7

thought the error message needs to be aligned in the context of the validation error from the `createRoot`

https://react.dev/reference/react-dom/client/hydrateRoot#hydrateroot

the options according to the doc shall take an Object for the corresponding React root

the actual error message shall be this way

```
 'Warning: You passed an options object as the second argument to `hydrateRoot(...)`, did you forget to pass a React element?',

```

or if someone passes a JSX element to options 

```
 'You passed a JSX element as an options to hydrateRoot. You probably meant to ' +
          'call root.render instead. ' +
          'Example usage:\n\n' +
          '  let root = hydrateRoot(domContainer, <App />, {...options});\n' +
          '  root.render(<App />);',
```

