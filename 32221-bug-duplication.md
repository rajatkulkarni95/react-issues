# Bug: duplication

> Issue #32221 - Created on 1/25/2025

> Original URL: https://github.com/facebook/react/issues/32221

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:

## Steps To Reproduce

1. Create a react commponents that uses objects key as Map or Set
2. re-render the commponents multi times
3. observe the behavior of the Map or Set
4. check for data access or updates due to objects duplication

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

https://www.reddit.com/r/reactjs/comments/120q19b/using_map_to_remove_duplicates_from_an_array_of/?rdt=57160
<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

is duplicate data 
## The expected behavior
that data be unique 

