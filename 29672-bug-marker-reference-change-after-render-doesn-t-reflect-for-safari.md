# Bug: Marker reference change after render doesn't reflect for Safari

> Issue #29672 - Created on 5/31/2024

> Original URL: https://github.com/facebook/react/issues/29672

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.0.0

## Steps To Reproduce

1. Use the latest version of Safari (for me it's Version 17.5 (19618.2.12.11.6)). This behavior doesn't occur for chrome/firefox.
2. Create an svg layout with any two markers, and a path element
3. Change the marker reference for `marker-end` of the path element from the first marker to the second one via a render cycle (in my example, triggered by setState)
4. Notice how the render cycle ("turn blue" in my code example) doesn't change the marker end 

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
[code-sandbox-link](https://codesandbox.io/p/sandbox/gallant-gagarin-9hmvgt?file=%2Fsrc%2FApp.js%3A32%2C25&layout=%257B%2522sidebarPanel%2522%253A%2522EXPLORER%2522%252C%2522rootPanelGroup%2522%253A%257B%2522direction%2522%253A%2522horizontal%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522id%2522%253A%2522ROOT_LAYOUT%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522UNKNOWN%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522clwtnd7iv00063b5vjlkvr6uc%2522%252C%2522sizes%2522%253A%255B100%252C0%255D%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522EDITOR%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522EDITOR%2522%252C%2522id%2522%253A%2522clwtnd7iv00023b5viontqixi%2522%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522direction%2522%253A%2522horizontal%2522%252C%2522id%2522%253A%2522SHELLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522SHELLS%2522%252C%2522id%2522%253A%2522clwtnd7iv00033b5vnt98kx96%2522%257D%255D%252C%2522sizes%2522%253A%255B100%255D%257D%255D%257D%252C%257B%2522type%2522%253A%2522PANEL_GROUP%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522direction%2522%253A%2522vertical%2522%252C%2522id%2522%253A%2522DEVTOOLS%2522%252C%2522panels%2522%253A%255B%257B%2522type%2522%253A%2522PANEL%2522%252C%2522contentType%2522%253A%2522DEVTOOLS%2522%252C%2522id%2522%253A%2522clwtnd7iv00053b5vm8zm54ta%2522%257D%255D%252C%2522sizes%2522%253A%255B100%255D%257D%255D%252C%2522sizes%2522%253A%255B50%252C50%255D%257D%252C%2522tabbedPanels%2522%253A%257B%2522clwtnd7iv00023b5viontqixi%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522clwtnd7iv00013b5vgoukubkr%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522filepath%2522%253A%2522%252Fsrc%252Findex.js%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%252C%257B%2522id%2522%253A%2522clwto3bed00023b5ul8p90qad%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522FILE%2522%252C%2522initialSelections%2522%253A%255B%257B%2522startLineNumber%2522%253A32%252C%2522startColumn%2522%253A25%252C%2522endLineNumber%2522%253A32%252C%2522endColumn%2522%253A25%257D%255D%252C%2522filepath%2522%253A%2522%252Fsrc%252FApp.js%2522%252C%2522state%2522%253A%2522IDLE%2522%257D%255D%252C%2522id%2522%253A%2522clwtnd7iv00023b5viontqixi%2522%252C%2522activeTabId%2522%253A%2522clwto3bed00023b5ul8p90qad%2522%257D%252C%2522clwtnd7iv00053b5vm8zm54ta%2522%253A%257B%2522tabs%2522%253A%255B%257B%2522id%2522%253A%2522clwtnd7iv00043b5vgji5ysdn%2522%252C%2522mode%2522%253A%2522permanent%2522%252C%2522type%2522%253A%2522UNASSIGNED_PORT%2522%252C%2522port%2522%253A0%252C%2522path%2522%253A%2522%252F%2522%257D%255D%252C%2522id%2522%253A%2522clwtnd7iv00053b5vm8zm54ta%2522%252C%2522activeTabId%2522%253A%2522clwtnd7iv00043b5vgji5ysdn%2522%257D%252C%2522clwtnd7iv00033b5vnt98kx96%2522%253A%257B%2522tabs%2522%253A%255B%255D%252C%2522id%2522%253A%2522clwtnd7iv00033b5vnt98kx96%2522%257D%257D%252C%2522showDevtools%2522%253Atrue%252C%2522showShells%2522%253Afalse%252C%2522showSidebar%2522%253Atrue%252C%2522sidebarPanelSize%2522%253A15%257D)

## Quick workaround

I found if you reset the key during the render cycle (i.e. `key={isBlue}` in the path element), the mount/unmount will cause the svg to render properly
