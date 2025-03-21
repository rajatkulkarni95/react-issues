# Bug: Invalid options to hydrateRoot can error with "This root received an early update"

> Issue #28792 - Created on 4/9/2024

> Original URL: https://github.com/facebook/react/issues/28792

## Description

## Overview

https://codesandbox.io/s/5ch3lc

If you call `hydrateRoot` with (container, options), so forgetting `<App />` and then call `root.render()`:

```js
const root = hydrateRoot(container, /* missing react element /* {
  onUncaughtError: (error) => {
   console.error(error);
  }
});

root.render();
```

## Result

We show this error:

```console
This root received an early update, before anything was able hydrate. Switched the entire root to client rendering.
```

This is common to do when switching from `createRoot` to `hydrateRoot`.

## Expected 

If you don't call `root.render()`, you see the real error:

```console
Objects are not valid as a React child (found: object with keys {onUncaughtError}). If you meant to render a collection of children, use an array instead.
```

But we should match the options validation error from `createRoot`:

```console
Warning: You passed a second argument to root.render(…) but it only accepts one argument.
```

With an error like:

```console
Warning: You passed an options object as the second argument to `hydrateRoot(...)`, did you forget to pass a React element?
```

## Versions
React version: 18.2.0 - 19.0.0-canary

