# Bug: use() hook

> Issue #28588 - Created on 3/19/2024

> Original URL: https://github.com/facebook/react/issues/28588

## Description

React version:
   "react": "0.0.0-experimental-4b84f1161-20240318",
   "react-dom": "0.0.0-experimental-4b84f1161-20240318",

1. How I can use the use() hook without Suspense component?
2. When I use the use() hook with Suspense and call API, I see it still calls the API many times (this version: 3 times, version: 0.0.0-experimental-a870b2d54-20240314 => 4 times).

Link code example: https://github.com/bradtraversy/react-19-playground/blob/main/src/components/useExample1/Joke.jsx
