# Bug: Rendering a list with duplicate keys causes unexpected behavior in reconciliation

> Issue #31608 - Created on 11/21/2024

> Original URL: https://github.com/facebook/react/issues/31608

## Description

Rendering a list with duplicate keys causes unexpected behavior in reconciliation. Not sure if this is a bug or not.

React version: v18.0.0

## Steps To Reproduce

1. Create a list of items with duplicate strings.
2. Render the list using map, assigning key directly as the string value of each item.
3. Use either useEffect or useLayoutEffect to update the list state after the component mounts.
4. Observe the DOM output when the state updates.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

```Jess
import { useLayoutEffect, useState } from "react";  

export default function App() {  
  const [items, setItems] = useState(["name2", "name3", "name4", "name4"]);  

  useLayoutEffect(() => {  
    setItems(["name1", "name2", "name3", "name4"]);  
  }, []);  

  return (  
    <div>  
      {items.map((item) => (  
        <div key={item}>{item}</div>  
      ))}  
    </div>  
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

When using either useEffect or useLayoutEffect:

The rendered DOM contains 5 items instead of 4. React fails to reconcile the list correctly due to duplicate keys, retaining an extra DOM node.


## The expected behavior

React should handle the state update and reconciliation correctly, ensuring that the rendered DOM contains only the updated list of items (4 items in this case). Duplicate keys should not lead to unexpected rendering issues.


