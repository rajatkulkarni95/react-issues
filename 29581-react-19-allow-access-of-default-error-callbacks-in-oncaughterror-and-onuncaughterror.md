# [React 19] Allow access of default error callbacks in `onCaughtError` and `onUncaughtError`

> Issue #29581 - Created on 5/24/2024

> Original URL: https://github.com/facebook/react/issues/29581

## Description

Hey React team! We at [Sentry](https://sentry.io/) have been working on adding support for the new `onCaughtError` and `onUncaughtError` root options in React 19 for error reporting.

Here's a PR I'm iterating on atm: [getsentry/sentry-javascript#12147](https://github.com/getsentry/sentry-javascript/pull/12147)

The API we are looking to add looks something like so:

```js
import { reactErrorHandler } from '@sentry/react';
import { hydrateRoot } from "react-dom/client";

ReactDOM.hydrateRoot(
  document.getElementById("root") as HTMLElement,
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  {
    onUncaughtError: reactErrorHandler(),
    onCaughtError: reactErrorHandler((error, errorInfo) => {
      // optional callback if users want more/custom config in addition?
    }),
  }
);
```
The only issue with `Sentry.reactErrorHandler` in the current form is that setting the `onUncaughtError` or `onCaughtError` options overrides the defaults for `onUncaughtError` and `onCaughtError`, which means you lose out on the dev mode logging like so:

https://github.com/facebook/react/blob/3ac551e855f9bec3161da2fc8787958aa62113db/packages/react-reconciler/src/ReactFiberErrorLogger.js#L36-L51

In this case there is no way for us to replicate the `An error occurred in the <${componentName}> component:` message (because `componentName` is private API), so asking users to add `Sentry.reactErrorHandler` degrades their local development experience.

This means if someone adds Sentry, or their own error logging via these hooks, they lose out on useful messaging in dev mode. We could recommend to users to make this production-only, but folks also use Sentry error reporting locally via [Spotlight, Sentry for development](https://spotlightjs.com/).

Is there a way we can get access to the original `onCaughtError` or `onUncaughtError` handler so we can execute that, while sending the error to Sentry at the same time? Or is there are alternate way we can design this API to make that happen?

Thanks!
