# `react-server-dom-webpack/node-register` not finding directives in IIFEs

> Issue #28961 - Created on 5/1/2024

> Original URL: https://github.com/facebook/react/issues/28961

## Description

## Summary

`react-server-dom-webpack/node-register` doesn't find `use client` directive in IIFEs.

Consider the following code
<details><summary>code</summary>

```js
(() => {
  "use strict";
  "use client";
  var __create = Object.create;
  var __defProp = Object.defineProperty;
  var __getOwnPropDesc = Object.getOwnPropertyDescriptor;
  var __getOwnPropNames = Object.getOwnPropertyNames;
  var __getProtoOf = Object.getPrototypeOf;
  var __hasOwnProp = Object.prototype.hasOwnProperty;
  var __name = (target, value) => __defProp(target, "name", {
    value,
    configurable: true
  });
  var __export = (target, all) => {
    for (var name in all) __defProp(target, name, {
      get: all[name],
      enumerable: true
    });
  };
  var __copyProps = (to, from, except, desc) => {
    if (from && typeof from === "object" || typeof from === "function") {
      for (let key of __getOwnPropNames(from)) if (!__hasOwnProp.call(to, key) && key !== except) __defProp(to, key, {
        get: () => from[key],
        enumerable: !(desc = __getOwnPropDesc(from, key)) || desc.enumerable
      });
    }
    return to;
  };
  var __toESM = (mod, isNodeMode, target) => (target = mod != null ? __create(__getProtoOf(mod)) : {}, __copyProps(isNodeMode || !mod || !mod.__esModule ? __defProp(target, "default", {
    value: mod,
    enumerable: true
  }) : target, mod));
  var __toCommonJS = mod => __copyProps(__defProp({}, "__esModule", {
    value: true
  }), mod);
  var Counter_client_exports = {};
  __export(Counter_client_exports, {
    Counter: () => Counter
  });
  module.exports = __toCommonJS(Counter_client_exports);
  var import_jsx_dev_runtime = require("react/jsx-dev-runtime");
  var React = __toESM(require("react"));
  console.log("Counter.client.tsx", React.useState);
  function Counter() {
    const [count, setCount] = React.useState(0);
    return (0, import_jsx_dev_runtime.jsxDEV)("div", {
      children: [(0, import_jsx_dev_runtime.jsxDEV)("h1", {
        children: "Counter"
      }, void 0, false, {
        fileName: "/Users/jackyef/Personal/Projects/beract/src/app/Counter.client.tsx",
        lineNumber: 17,
        columnNumber: 7
      }, this), (0, import_jsx_dev_runtime.jsxDEV)("p", {
        children: ["Count: ", count]
      }, void 0, true, {
        fileName: "/Users/jackyef/Personal/Projects/beract/src/app/Counter.client.tsx",
        lineNumber: 18,
        columnNumber: 7
      }, this), (0, import_jsx_dev_runtime.jsxDEV)("button", {
        onClick: () => setCount(c => c + 1),
        children: "Increment"
      }, void 0, false, {
        fileName: "/Users/jackyef/Personal/Projects/beract/src/app/Counter.client.tsx",
        lineNumber: 19,
        columnNumber: 7
      }, this)]
    }, void 0, true, {
      fileName: "/Users/jackyef/Personal/Projects/beract/src/app/Counter.client.tsx",
      lineNumber: 16,
      columnNumber: 5
    }, this);
  }
  __name(Counter, "Counter");
})();
```

</details>

[This loop](https://github.com/facebook/react/blob/4508873393058e86bed308b56e49ec883ece59d1/packages/react-server-dom-webpack/src/ReactFlightWebpackNodeRegister.js#L53-L64) will not find the `use client` directive because it isn't searching deep enough.

Is this an expected behavior?

For what it's worth, I am not yet using Webpack to do compilation here, I am using [`tsx watch`](https://github.com/privatenumber/tsx) for fast setup.
```
"react": "19.0.0-canary-e3ebcd54b-20240405",
"react-dom": "19.0.0-canary-e3ebcd54b-20240405",
"react-server-dom-webpack": "19.0.0-canary-e3ebcd54b-20240405",
```
