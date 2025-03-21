# Bug: React 18.3 warning says to import `act` from `react`, only `unstable_act` exists

> Issue #28915 - Created on 4/26/2024

> Original URL: https://github.com/facebook/react/issues/28915

## Description

In the newly released 18.3.0 release, if you try to use the `act` function from `react-dom/test-utils`, you will get the following warning:

> Import `act` from `react` instead of `react-dom/test-utils`

However, the 18.3.0 release only ships `unstable_act`, not `act`. The react 19 beta seems to have renamed to `act`.
I feel the warning should either tell you to import from `unstable_act`, _or_ the `act` export should actually exist, even if aliased to `unstable_act` internally

React version: 18.3.0

## Steps To Reproduce

1. On react + react-dom@18.3.0, import and use `act` from `react-dom/test-utils`.
2. See warning
3. Try to import `act` from react@18.3.0

Link to code example: [https://codesandbox.io/p/sandbox/intelligent-chandrasekhar-p9xk7h](https://codesandbox.io/p/sandbox/intelligent-chandrasekhar-p9xk7h?file=%2Fsrc%2Ftest.js%3A6%2C1&layout=%257B%2522sidebarPanel%2522%253A%2522EXPLORER%2522%252C%2522rootPanelGroup%2522%253A%257B%2522direction%2522%253A%2522horizontal%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522id%2522%253A%2522ROOT_LAYOUT%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522clvfsslh200063b6joqedrppd%2522%252C%2522sizes%2522%253A%255B100%252C0%255D%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522EDITOR%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522id%2522%253A%2522clvfsslh200023b6jmbhhjfwu%2522%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522SHELLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522id%2522%253A%2522clvfsslh200033b6jhy11k8p6%2522%257D%255D%252C%2522sizes%2522%253A%255B100%255D%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522DEVTOOLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522id%2522%253A%2522clvfsslh200053b6jdt7slm5u%2522%257D%255D%252C%2522sizes%2522%253A%255B100%255D%257D%255D%252C%2522sizes%2522%253A%255B50%252C50%255D%257D%252C%2522tabbedPanels%2522%253A%257B%2522clvfsslh200023b6jmbhhjfwu%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522clvfsslh200013b6j2ebpwwn7%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522filepath%2522%253A%2522%252Fsrc%252Findex.js%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%252C%257B%2522id%2522%253A%2522clvfst1ny003t3b6janff2rkm%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522initialSelections%2522%253A%255B%257B%2522startLineNumber%2522%253A5%252C%2522startColumn%2522%253A18%252C%2522endLineNumber%2522%253A5%252C%2522endColumn%2522%253A18%257D%255D%252C%2522filepath%2522%253A%2522%252Fpackage.json%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%252C%257B%2522id%2522%253A%2522clvfszp0000023b6ijbh4phsw%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522initialSelections%2522%253A%255B%257B%2522startLineNumber%2522%253A6%252C%2522startColumn%2522%253A1%252C%2522endLineNumber%2522%253A6%252C%2522endColumn%2522%253A1%257D%255D%252C%2522filepath%2522%253A%2522%252Fsrc%252Ftest.js%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%255D%252C%2522id%2522%253A%2522clvfsslh200023b6jmbhhjfwu%2522%252C%2522activeTabId%2522%253A%2522clvfszp0000023b6ijbh4phsw%2522%257D%252C%2522clvfsslh200053b6jdt7slm5u%2522%253A%257B%2522id%2522%253A%2522clvfsslh200053b6jdt7slm5u%2522%252C%2522activeTabId%2522%253A%2522clvfsxdrw00fk3b6iv08mk34s%2522%252C%2522tabs%2522%253A%255B%257B%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%252C%2522id%2522%253A%2522clvfsxdrw00fk3b6iv08mk34s%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522path%2522%253A%2522%252F%2522%257D%255D%257D%252C%2522clvfsslh200033b6jhy11k8p6%2522%253A%257B%2522tabs%2522%253A%255B%255D%252C%2522id%2522%253A%2522clvfsslh200033b6jhy11k8p6%2522%257D%257D%252C%2522showDevtools%2522%253Atrue%252C%2522showShells%2522%253Afalse%252C%2522showSidebar%2522%253Atrue%252C%2522sidebarPanelSize%2522%253A15%257D)

## The current behavior

`act` does not exist, warning tells you to use it

## The expected behavior

`act` exists, warning tells you to use it _OR_ warning tells you to use `unstable_act`
