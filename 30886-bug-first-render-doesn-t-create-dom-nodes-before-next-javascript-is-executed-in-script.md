# Bug: First render doesn't create DOM nodes before next javascript is executed in script

> Issue #30886 - Created on 9/5/2024

> Original URL: https://github.com/facebook/react/issues/30886

## Description

This may have been discussed elsewhere but I wasn't able to find anything. 

With the update to using `createRoot` in React 18, the DOM is created asynchronously, which means any code running after `root.render()` cannot depend on the DOM that React is creating.

React version: 18.2.0

## Steps To Reproduce

```js
const root = ReactDOM.createRoot(document.getElementById("app"));
root.render(
    React.createElement("div", { id: "reactChild" }, "Rendered By React")
);

document.getElementById("reactChild").innerHTML = "Replaced By VanillaJS"; // this errors
```

## The current behavior
 JS will error because `document.getElementById("reactChild")` is null and not found

## The expected behavior
React will render first and then `document.getElementById("reactChild")` will execute find the node


[Link to code example](https://codesandbox.io/p/sandbox/2njxcj?layout=%257B%2522sidebarPanel%2522%253A%2522EXPLORER%2522%252C%2522rootPanelGroup%2522%253A%257B%2522direction%2522%253A%2522horizontal%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522id%2522%253A%2522ROOT_LAYOUT%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522cm0p0a5am00063b6igau3mza0%2522%252C%2522sizes%2522%253A%255B100%255D%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522EDITOR%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522id%2522%253A%2522cm0p0a5am00023b6i7pymhzso%2522%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522SHELLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522id%2522%253A%2522cm0p0a5am00033b6i48103piz%2522%257D%255D%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522DEVTOOLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522id%2522%253A%2522cm0p0a5am00053b6i9ksfo73k%2522%257D%255D%257D%255D%252C%2522sizes%2522%253A%255B50%252C50%255D%257D%252C%2522tabbedPanels%2522%253A%257B%2522cm0p0a5am00023b6i7pymhzso%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0p0a5am00013b6i0zwjrq7t%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522filepath%2522%253A%2522%252Findex.html%2522%252C%2522state%2522%253A%2522IDLE%2522%252C%2522initialSelections%2522%253A%255B%257B%2522startLineNumber%2522%253A20%252C%2522startColumn%2522%253A1%252C%2522endLineNumber%2522%253A20%252C%2522endColumn%2522%253A1%257D%255D%257D%255D%252C%2522id%2522%253A%2522cm0p0a5am00023b6i7pymhzso%2522%252C%2522activeTabId%2522%253A%2522cm0p0a5am00013b6i0zwjrq7t%2522%257D%252C%2522cm0p0a5am00053b6i9ksfo73k%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0p0a5am00043b6iord4hwnv%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%257D%255D%252C%2522id%2522%253A%2522cm0p0a5am00053b6i9ksfo73k%2522%252C%2522activeTabId%2522%253A%2522cm0p0a5am00043b6iord4hwnv%2522%257D%252C%2522cm0p0a5am00033b6i48103piz%2522%253A%257B%2522tabs%2522%253A%255B%255D%252C%2522id%2522%253A%2522cm0p0a5am00033b6i48103piz%2522%257D%257D%252C%2522showDevtools%2522%253Atrue%252C%2522showShells%2522%253Afalse%252C%2522showSidebar%2522%253Atrue%252C%2522sidebarPanelSize%2522%253A15%257D)


Is this just an expected result with React 18+? If you fallback and use `ReactDOM.render()` instead, it works as expected.
