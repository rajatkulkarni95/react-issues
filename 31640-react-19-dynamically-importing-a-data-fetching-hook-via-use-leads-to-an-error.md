# [React 19] Dynamically importing a data fetching hook via `use()` leads to an error

> Issue #31640 - Created on 11/28/2024

> Original URL: https://github.com/facebook/react/issues/31640

## Description

### Describe the bug

I've been trying to create a component which would encapsulate data loading logic, to have the most granular approach to using `<Suspense/>`, avoiding UI duplication with skeletons. My goal was to have _one component_ which would handle suspending, fallback UI, loading, polling, errors, etc, and be used in a _server component_ like so:

```
 <AsyncValue
    query={useSomeQuery} // query wrapper fn or potentially a query wrapper fn name string 
    queryProps={{
        itemId: "0001", // optional query props 
    }}
    dataKey="name" // optional accessor to a value which `extends ReactNode` in case an object is returned 
    render={Value} // Some valid React compoennt 
/>
```

This, **afaik**, would result in everything but the suspended value being pre-rendered server-side, eliminating the need to care about large skeletons, duplicating layout components or what not. Thought that would be neat?

I have arrived at a working solution, but a hacky one, as it used `throw` to trigger `<Suspense />`. When it struck me that we now have the `use()` hook to handle exactly what I thought was needed – keeping a component suspended while dynamically importing a hook. However, when I tried using it I saw: 

`Error: Update hook called on initial render. This is likely a bug in React. Please file an issue.`

Even though it seems to function. The data fetch is fired on the server, response is streamed to the client, where the hook proceeds to poll and update the value.

TLDR:

- Is dynamically importing hooks even viable or it ruins some logic under the hood?
- If is is viable, can it be done via a `use()` hook to trigger `<Suspense />` boundaries?

### Reproducible example

https://codesandbox.io/p/devbox/6xmt4y

### Expected behavior

Work with `use()` like it does without it.

### React version

19.0.0-rc-2d16326d-20240930

### Related issue

https://github.com/TanStack/query/issues/8362


