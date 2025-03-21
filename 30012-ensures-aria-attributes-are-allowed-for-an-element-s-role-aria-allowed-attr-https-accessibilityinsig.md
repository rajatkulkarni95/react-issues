# Ensures ARIA attributes are allowed for an element's role (aria-allowed-attr - https://accessibilityinsights.io/info-examples/web/aria-allowed-attr)Bug: 

> Issue #30012 - Created on 6/21/2024

> Original URL: https://github.com/facebook/react/issues/30012

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
Ensures ARIA attributes are allowed for an element's role (aria-allowed-attr - https://accessibilityinsights.io/info-examples/web/aria-allowed-attr)

Element path: .b-filter-bar-enabled

 

Snippet: <div class="b-grid-header b-level-0 b-depth-0 b-last-leaf b-filter-bar-enabled" role="presentation" aria-sort="none" aria-label="SPACE for context menu" data-column-id="b-scheduler-1-col-1" data-column="_verticalTimeAxis2" style="min-width: 0px; flex: 1 1 0%;" aria-colindex="1">

![224570_AI4W](https://github.com/facebook/react/assets/93735775/e17de8f2-2611-41b9-bdf3-a889d0862326)


## The expected behavior
ARIA attributes are not allowed: aria-sort="none", aria-colindex="1"
