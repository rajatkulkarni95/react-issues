# Bug: Displayed content is not handled properly. 

> Issue #29168 - Created on 5/19/2024

> Original URL: https://github.com/facebook/react/issues/29168

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->
At the "Adding Interactivity" section of the React documentation, under "State: a component’s memory," there are 12 content items to show. When clicking on "show details" for the first content item (1/12), the displayed content is not static, unlike the others.


React version:
v18.3.1

## Steps To Reproduce

1. Go to Home page of the react [https://react.dev/](https://react.dev/)
2. Click on Learn React
3. Navigate to "Adding Interactivity"
4. Scroll to "State: a component’s memory"
5. Click on "show details" for the first content item (1/12)


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

https://github.com/facebook/react/assets/99067547/b87f8b01-4ac9-42a2-9553-ff3ea0c89800



<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
* Browser: Chrome
* Operating System: Windows 11
* Device: HP Pavilion Laptop
* Screen Resolution: 100%

## The expected behavior
The displayed content should remain static, consistent with the behavior of the other content items.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->



<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->
## Additional Notes
This issue was observed on Chrome Browser in Windows 11 on an HP Pavilion Laptop with a screen resolution set to 100%.

