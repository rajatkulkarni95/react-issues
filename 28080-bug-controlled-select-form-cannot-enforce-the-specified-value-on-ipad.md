# Bug: Controlled `<select>` form cannot enforce the specified "value" on iPad.

> Issue #28080 - Created on 1/25/2024

> Original URL: https://github.com/facebook/react/issues/28080

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18

## Steps To Reproduce

1. Open https://playcode.io/1737391 on iPad (not iPhone) Safari. I've confirmed on iPadOS 16.4.
2. Select "No1" from the select box. An alert is shown and the select box is kept to be "Please select". 
3. Select "No1" again. 

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

https://playcode.io/1737391

```jsx
import React from 'react';

export function App(props) {
  return (
    <select value="-1" onChange={(ev) => { alert(ev.target.selectedIndex) }}>
      <option value="-1">Please select</option>
      <option value="1">No1</option>
      <option value="2">No2</option>
      <option value="3">No3</option>
    </select>
  );
}
```

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

After the step 3, the select box will be changed to "No1".

## The expected behavior

The select box should be kept to "Please select". 

Other browsers other than iPad (e.g. iPhone Safari, Windows Chrome and mac Safari works well. This issue is reproduced only on iPad.
