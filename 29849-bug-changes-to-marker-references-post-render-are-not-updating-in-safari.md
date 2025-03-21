# Bug:  Changes to marker references post-render are not updating in Safari

> Issue #29849 - Created on 6/11/2024

> Original URL: https://github.com/facebook/react/issues/29849

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.0.0
## Steps To Reproduce

1. Ensure you are using the most recent version of Safari, which is currently Version 17.5 (19618.2.12.11.6). The issue described does not manifest in Chrome or Firefox.
2. Construct an SVG layout that includes two distinct markers along with a path element.
3. Modify the marker-end attribute of the path element, switching from the first marker to the second, through a rendering cycle. This can be initiated by a state change (as demonstrated in my example, using setState).
4. Observe that the rendering cycle, which should alter the marker end color to blue (as per my code example), fails to update the marker end.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

