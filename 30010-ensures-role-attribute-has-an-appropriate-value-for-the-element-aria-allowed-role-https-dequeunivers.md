# Ensures role attribute has an appropriate value for the element (aria-allowed-role - https://dequeuniversity.com/rules/axe/4.7/aria-allowed-role?application=msftAI)

> Issue #30010 - Created on 6/21/2024

> Original URL: https://github.com/facebook/react/issues/30010

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 16.14.0

## Steps To Reproduce

1. Launch the application using URL: [Bryntum Scheduler - Vertical mode demo (React)](https://www.bryntum.com/products/scheduler/examples/frameworks/react/javascript/vertical/build/).
2. “Vertical mode demo (React)” screen should open.
3. TAB to “Filter Event” button.
4. Run AI4W fast pass and observe the issue.

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
Ensures role attribute has an appropriate value for the element (aria-allowed-role - https://dequeuniversity.com/rules/axe/4.7/aria-allowed-role?application=msftAI)

 

Element path: .b-grid-header-container

Snippet: <header role="row" aria-rowindex="1" class="b-grid-header-container b-show-yscroll-padding" data-owner-cmp="b-scheduler-1" data-max-depth="0">

![224479_AI4W](https://github.com/facebook/react/assets/93735775/68209366-b799-4efd-9f08-0d078a50e6e4)



## The expected behavior
ARIA role row is not allowed for given element

