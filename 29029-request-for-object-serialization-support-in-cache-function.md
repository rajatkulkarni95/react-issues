# Request for Object Serialization Support in cache() Function

> Issue #29029 - Created on 5/9/2024

> Original URL: https://github.com/facebook/react/issues/29029

## Description

Is there any plan to support object serialization in [`cache()`](https://react.dev/reference/react/cache) function similar to how modern data fetching libraries handle caching?

### Current Behavior
Currently, React's caching mechanism supports only primitive values. This limitation becomes inconvenient when handling multiple properties, necessitating a workaround to manually serialize objects.

React Cache uses a [`WeakMap` to compare object references](https://github.com/facebook/react/blob/ec15267a001086deb4ab5412d3f8b7e13573d6a5/packages/react/src/ReactCacheImpl.js#L85-L91), requiring the same object reference to utilize caching effectively.

In previous cache implementations, it was possible to [pass a function that serializes keys into strings](https://github.com/facebook/react/blob/ec15267a001086deb4ab5412d3f8b7e13573d6a5/packages/react-cache/src/ReactCacheOld.js#L147). Is there any plan to readopt this approach?

### Examples from Other Libraries
- **SWR:** [Since SWR 1.1.0, object-like keys will be serialized under the hood automatically.](https://swr.vercel.app/docs/arguments#passing-objects)
- **TanStack Query:** Allows for [object keys](https://tanstack.com/query/latest/docs/framework/react/guides/query-keys#query-keys-are-hashed-deterministically) and [provides an option to pass a custom serialization function](https://github.com/TanStack/query/discussions/477#discussioncomment-2152436) for unsupported types, making it adaptable for various data fetching scenarios.

Looking forward to your thoughts!

