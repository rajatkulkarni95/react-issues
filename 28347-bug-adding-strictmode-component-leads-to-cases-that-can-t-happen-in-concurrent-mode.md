# Bug: Adding StrictMode component leads to cases that can't happen in concurrent mode. 

> Issue #28347 - Created on 2/15/2024

> Original URL: https://github.com/facebook/react/issues/28347

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

I'm currently preparing my app for the new react 18 features and turned on the new StrictMode component. 
According to the docs it's a good way to make sure our apps are ready for concurrent mode and avoids side effects. 
https://react.dev/blog/2022/03/08/react-18-upgrade-guide
I know that all useEffects are called twice. It does makes sense and helps to catch some side effects. 
It turned out that some libraries are not ready for it though. For instance useEffect with empty dep array is also called twice. 
That means that we can't really treat returned callback of such useEffect as willUnmount method. 
From what I understand it will prepare us for the future  offscreen API and open new doors for future performance improvement. 
That's great. But At the moment I want to just make sure my app supports concurrent mode as a lot of libraries are not ready for missing willUnmount (I know that if useEffect would be symmetrical that wouldn't be an issue but it is in a lot of libs :D ).

**Is it really possible that useEffect with empty array can be called twice with reserving the component state in concurrent mode? 
(Without the offscreen API)?**

One of the libs I use has a ref (const wasUnmountedAndCancelledAllFetchCalls = useRef(false)) and that flag is changed in willMount (return callback of the useEffect with empty dep array). It seems to be safe for the concurrent mode as if we drop a render progress due to more important update (or a new transition) we won't call willUnmount unless we actually unmounted the component as it happened in the commit phase which is synchronous. Am I wrong here?

I would really really appreciate all responses 🥹. 
React version: latest

## Steps To Reproduce

1. Add StrictMode Component 
2. UseEffect with empty deps array is called twice in Concurrent mode

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

UseEffect called twice

## The expected behavior

UseEffect called twice if that scenario is actually possible in concurrent mode or StrictMode having a flag that tells if he should test against offscreen rendering. 

