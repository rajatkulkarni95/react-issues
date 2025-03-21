# Bug: Empty `style={}` object values cause hydration warnings in React 18.3.1 - Includes solution

> Issue #30163 - Created on 7/1/2024

> Original URL: https://github.com/facebook/react/issues/30163

## Description

# Issue

Hydrating a React 18 application with a `style={}` prop object with empty values results in a hydration warning:

```jsx
function App() {
  const style = {
    color: "red",
    // Empty style value i.e. from conditional assignment.
    "--empty-custom-property": "",
  };

  return <p style={style}>Hello World</p>;
}
```

![CleanShot 2024-07-01 at 21 07 54@2x](https://github.com/facebook/react/assets/199204/ec058002-4f15-4725-87d1-dd0a3beca074)

Repro: https://github.com/nandastone/react-18-19-ssr-empty-style

In the example above, the client generates a style object containing a property with an empty string value. This does not match the expected ReactDOM behavior which discards style object properties with empty values:

![CleanShot 2024-07-01 at 21 01 47@2x](https://github.com/facebook/react/assets/199204/996a4f8c-62f0-4b00-bbb1-2b714e0948c3)

Example: https://codesandbox.io/p/sandbox/objective-tesla-nzsvwz?file=%2Fsrc%2FApp.js%3A8%2C1

#  Culprit

The issue lies in a line in the development-mode hydration check, called during `diffHydratedProperties()`: [CSSPropertyOperations.js#L33](https://github.com/facebook/react/blob/v18.3.1/packages/react-dom/src/client/CSSPropertyOperations.js#L33)

This check does not match the stricter ReactDOM implementation that correctly discards properties with empty values: [dangerousStyleValue.js#L31](https://github.com/facebook/react/blob/v18.3.1/packages/react-dom/src/shared/dangerousStyleValue.js#L31)

# Solution

Update `createDangerousStringForStyles()` to match the ReactDOM implementation. This was addressed in React 19: [CSSPropertyOperations.js#L34](https://github.com/facebook/react/blob/main/packages/react-dom-bindings/src/client/CSSPropertyOperations.js#L34).

However, many applications (including mine) will be using React 18 for a while, so it would be good to fix this issue. Although the contributing guidelines suggest that all PRs should target `main`, is there a way to open a PR targeting the v18.3.1 tag?

React version: 18.3.1

## Steps To Reproduce

1. Render a component with a style prop where the object has a property with empty string value.
2. Render the app using a React 18 server API e.g. `renderToPipeableStream()`.
3. Hydrate the app.

Link to code example:

https://github.com/nandastone/react-18-19-ssr-empty-style

1. Clone.
2. `yarn`
3. `yarn start`
4. http://localhost:9000

Unfortunately Codesandbox/Stackblitz were proving difficult to properly setup the SSR example.

## The current behavior

Receive hydration warning.

## The expected behavior

Should not receive hydration warning.

