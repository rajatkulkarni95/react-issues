# Bug: Ref is set after componentDidMount (when mixing Class and Functional components)

> Issue #29897 - Created on 6/14/2024

> Original URL: https://github.com/facebook/react/issues/29897

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

```javascript
import React, { PureComponent, useCallback, useEffect } from 'react';

export function App(props) {
  const refCallback = (ref) => {
    console.log("Reference received")
  };

  return (
    <div ref={refCallback}>
        <ClassComponent  />
        <FunctionalComponent />
    </div>
  );
}

class ClassComponent extends PureComponent {
  componentDidMount() {
    console.log("ClassComponent mounted")
  }
  render() {
    return "ClassComponent"
  }
}


function FunctionalComponent() {
  useEffect(() => {
    console.log("FunctionalComponent mounted")
  })
  return "FunctionalComponent"
}
```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://playcode.io/1905766

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Console logs:

```
ClassComponent mounted
Reference received
FunctionalComponent mounted
```

`ClassComponent` is mounted before reference is received. It's different if a functional component is used.

## The expected behavior

I'm not sure if this is expected behavior but I was expecting to receive a ref before components are mounted.

```
Reference received
ClassComponent mounted
FunctionalComponent mounted
```
