# [React 19] react-is isFragment doesn't worked

> Issue #31688 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31688

## Description

Project use react version is 17.0.2 and not fixed version for react-is
To fix bug: now I fixed the react-is version to 17.0.2 in package.json , or else it will autoupgrade to  the latest version 19.0.0

react-is version 19.0.0

### Steps To Reproduce

```jsx
import { isFragment } from "react-is";  

const fragment = <></>;
console.log("isFragment", isFragment(fragment));
```

## The current behavior

```jsx
// isFragment false
```

## The expected behavior

```jsx
// isFragment true
```


