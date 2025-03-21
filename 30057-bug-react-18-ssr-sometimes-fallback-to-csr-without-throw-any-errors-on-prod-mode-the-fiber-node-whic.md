# Bug: React 18 SSR Sometimes fallback to CSR without throw any errors on Prod Mode, The fiber node which tag is "HostRoot"（3）has flags "Snapshot"（1024），it works fine when flags is Update(4)

> Issue #30057 - Created on 6/24/2024

> Original URL: https://github.com/facebook/react/issues/30057

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:18 
this bug only happen on Production mode, it works fine on Development mode 

## Steps To Reproduce

1. Refreshing My Website to view the SSR skeleton content，the link is https://jimeng.jianying.com/ai-tool/home
3. Sometimes it works fined, but Sometimes the page become black  after SSR skeleton content（we can 4x slower cpu to meet this），I found it's because My SSR content inside "div#root" is removed by this code:
![image](https://github.com/facebook/react/assets/22492458/e3ee2132-d190-4966-8908-9525b572c849)
4. It seems that the fiber node has Snapshot(1024) flags, which should be "Update"（4）。I don't know the reason, and why sometimes it works fine, somethimes it works wrong
5. the source code error stack is inside react repo: packages/react-reconciler/src/ReactFiberCommitWork.js，commitBeforeMutationEffectsOnFiber Function

More info: our project using ssr to show skeleton,  but we don't want "hydrating", our client side render will return "null" to skip react hydrating. 


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
somethimes the fiber node has flag "Snapshot"（1024）, which causing my ssr content is removed

## The expected behavior
the fiber node's flag  is always "Update"（4）, which won't remove my ssr content 

