# [React 19] Can we get top-level funciton imports without being prefixed with `use` to be more semantic?

> Issue #29048 - Created on 5/13/2024

> Original URL: https://github.com/facebook/react/issues/29048

## Description

By convention, everyone creates hooks named `useX`. Then we call it to get some stuff. That stuff can include other functions:

```
import { useTenant } from "globalization"

const SomeComponent = () => {
     const { getCurrentTenant } = useTenant();
}
```

Can we get closer to this code in React 19?

```
import { getCurrentTenant } from "globalization"

const SomeComponent = () => {
}
```

That `const { getCurrentTenant } = useTenant();` is boilerplate.

P.S. Because I could not find a place to discuss features, I had to send this issue here.
