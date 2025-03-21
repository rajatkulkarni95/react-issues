# Bug: useMemo has a problem of executing  multiple times without changing dependencies

> Issue #30955 - Created on 9/13/2024

> Original URL: https://github.com/facebook/react/issues/30955

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
    "react": "18.3.0-canary-9377e1010-20230712",
    "react-dom": "18.3.0-canary-9377e1010-20230712",

## Steps To Reproduce
[Demo](https://codesandbox.io/p/sandbox/react-dev-forked-48kvw3?layout=%257B%2522sidebarPanel%2522%253A%2522EXPLORER%2522%252C%2522rootPanelGroup%2522%253A%257B%2522direction%2522%253A%2522horizontal%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522id%2522%253A%2522ROOT_LAYOUT%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522cm0yptg7a0006356miyz225ki%2522%252C%2522sizes%2522%253A%255B100%255D%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522EDITOR%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522id%2522%253A%2522cm0yptg7a0002356mynkuav8y%2522%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522SHELLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522id%2522%253A%2522cm0yptg7a0003356meps87olz%2522%257D%255D%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522DEVTOOLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522id%2522%253A%2522cm0yptg7a0005356mc3mp4kdr%2522%257D%255D%257D%255D%252C%2522sizes%2522%253A%255B50%252C50%255D%257D%252C%2522tabbedPanels%2522%253A%257B%2522cm0yptg7a0002356mynkuav8y%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0yptg790001356mq1gbd58m%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522filepath%2522%253A%2522%252Fsrc%252Findex.js%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%255D%252C%2522id%2522%253A%2522cm0yptg7a0002356mynkuav8y%2522%252C%2522activeTabId%2522%253A%2522cm0yptg790001356mq1gbd58m%2522%257D%252C%2522cm0yptg7a0005356mc3mp4kdr%2522%253A%257B%2522id%2522%253A%2522cm0yptg7a0005356mc3mp4kdr%2522%252C%2522activeTabId%2522%253A%2522cm103o7yv0019356mbw9nl37y%2522%252C%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522cm0yptg7a0004356mopnriwu6%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%257D%252C%257B%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%252C%2522id%2522%253A%2522cm103o7yv0019356mbw9nl37y%2522%252C%2522mode%2522%253A%2522permanent%2522%257D%255D%257D%252C%2522cm0yptg7a0003356meps87olz%2522%253A%257B%2522tabs%2522%253A%255B%255D%252C%2522id%2522%253A%2522cm0yptg7a0003356meps87olz%2522%257D%257D%252C%2522showDevtools%2522%253Atrue%252C%2522showShells%2522%253Afalse%252C%2522showSidebar%2522%253Atrue%252C%2522sidebarPanelSize%2522%253A15%257D)

1. After running, click the Posts button, and you will see multiple outputs in the log executing the memo function

2. It should be noted that if you remove async and await from then, then there will be no phenomenon of executing the memo function multiple times
3. This demo forked from [useTransition](https://react.dev/reference/react/useTransition )and modified the logic of PostsTab

![image](https://github.com/user-attachments/assets/0738bcfb-7fca-47eb-90bf-bbeb3bf0b4db)

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


## The expected behavior

