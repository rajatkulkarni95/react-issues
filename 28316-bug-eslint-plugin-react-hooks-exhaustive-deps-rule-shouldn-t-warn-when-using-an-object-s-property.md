# Bug: eslint-plugin-react-hooks `exhaustive-deps` rule shouldn't warn when using an object's property

> Issue #28316 - Created on 2/13/2024

> Original URL: https://github.com/facebook/react/issues/28316

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

eslint-plugin-react-hooks version: 4.6.0

## Example code:
```js
import { useCallback } from "react";
import { useFetcher } from "react-router-dom";

...
    const fetcher = useFetcher();
    const onClick = useCallback(() => fetcher.submit(XXX), [fetcher.submit]);
    //  warning  React Hook useCallback has a missing dependency: 'fetcher'. Either include it or remove the dependency array  react-hooks/exhaustive-deps
```

This is the recommended way of specifying the dependency for this method, see https://github.com/remix-run/react-router/pull/10336.

## Expected
There's no warning.

Thanks!
