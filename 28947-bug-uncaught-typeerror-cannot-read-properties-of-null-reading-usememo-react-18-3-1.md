# Bug: Uncaught TypeError: Cannot read properties of null (reading 'useMemo') [React 18.3.1]

> Issue #28947 - Created on 4/29/2024

> Original URL: https://github.com/facebook/react/issues/28947

## Description

I have upgraded to React `18.3.1`, previously from `18.2.0`. After upgrading, my app won't start. At first it's due to `useMemo` in `<PortalProvider />` which is a component from `blueprintjs`. When I open the file, it looks something like:
```js
import * as React from "react";

const PortalProvider = (...) => {
    const data = React.useMemo(...)
}
```
From the error message, here I'm assuming `React` is null, but I'm not sure why. This was working fine before with `18.2.0`. I tried removing this `<PortalProvider />` component, but I get another error in `<Provider />` from `react-redux`, but this time instead of `useMemo`, it errors out with `useContext`. All I did was upgrade the React version nothing else. Am I missing something? I would like to upgrade to `18.3.1` to prepare for React 19.

React version: `18.3.1`
Blueprintjs version: `5.10.2`
Redux version: `4.2.1`
React-redux version `8.1.3`

![Screenshot of console](https://github.com/facebook/react/assets/75826315/965c1445-b5c3-41c7-a19e-aa30b5862994)

My `src/index.tsx`:
```tsx
import { useEffect } from "react";
import {
  createRoutesFromChildren,
  matchRoutes,
  useLocation,
  useNavigationType,
} from "react-router-dom";
import { Classes, PortalProvider } from "@blueprintjs/core";
import { createRoot } from "react-dom/client";
import * as Sentry from "@sentry/react";
import "style/index.scss";
import Router from "./router";
import store from "redux/store";
import { Provider } from "react-redux";
import { APP_VERSION } from "utils/constants";
import * as serviceWorker from "./serviceWorker";

Sentry.init({
  dsn: "...",
  integrations: [
    Sentry.reactRouterV6BrowserTracingIntegration({
      useEffect: useEffect,
      useLocation,
      useNavigationType,
      createRoutesFromChildren,
      matchRoutes,
    }),
    Sentry.replayIntegration(),
  ],
  enabled: process.env.NODE_ENV !== "development",
  release: APP_VERSION.toString(),
  // Set tracesSampleRate to 1.0 to capture 100%
  // of transactions for performance monitoring.
  // We recommend adjusting this value in production
  tracesSampleRate: 1.0,
});

// <React.StrictMode> removed because of blueprint https://github.com/palantir/blueprint/issues/3979
const container = document.getElementById("root");
if (!container) throw new Error("Element with id 'root' not found.");
container.classList.add(Classes.DARK);

const root = createRoot(container);
root.render(
  <PortalProvider portalClassName={Classes.DARK}>
    <Provider store={store}>
      <Router />
    </Provider>
  </PortalProvider>
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```
