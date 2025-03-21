# Bug: React 19 can't hydrate into root <html>

> Issue #32017 - Created on 1/8/2025

> Original URL: https://github.com/facebook/react/issues/32017

## Description

React version: 19.0.0

## Steps To Reproduce

1. `hydrateRoot(document.documentElement, <html lang="ab"></html>)`

Error:

```
installHook.js:1 In HTML, <html> cannot be a child of <html>.
This will cause a hydration error.
```

## The current behavior

Now that React 19 handles hoisting, rendering the entire <html> is desirable. But in order to hydrate or render on client, you need to pass it a root node, and it will attempt to render your root html below the actual html node. 


## The expected behavior

I think this could be a special case in React where `if (rootElement.type === 'html' && rootNode.type === 'HTML')` it avoids this error and just "controls" the root html element.
