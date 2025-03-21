# Unable to select color using voice access commands.

> Issue #29826 - Created on 6/10/2024

> Original URL: https://github.com/facebook/react/issues/29826

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 16.8.0

**Pre-Requisites**
Settings->Accessibility->Voice Access

## Steps To Reproduce

1. Open [React Select (react-select.com)](https://react-select.com/home).
2. Navigate to the welcome 'Getting Started' page.
3. Expand 'Multi' dropdown.
4. Give command as 'Click <<color name>> and observe.

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
No action is performed upon announcing category color. Voice Access displayed as left clicked <category name>.

[voice access-numbers-react.webm](https://github.com/facebook/react/assets/93735775/1a45a68a-f2e7-4e35-b127-f57f3d46061d)

[react-voice acess.webm](https://github.com/facebook/react/assets/93735775/916f0ef3-64e5-4090-ab57-d5ad4c04128d)

## The expected behavior
Category should be select properly with voice access command.


