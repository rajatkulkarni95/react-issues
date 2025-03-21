# Bug: Conditionally rendering a lazy loaded component only after the parent node is attached causes infinite loop

> Issue #30582 - Created on 8/2/2024

> Original URL: https://github.com/facebook/react/issues/30582

## Description

React version: 18.3.1 and [19.0.0-rc-b57d2823-20240822](https://codesandbox.io/p/sandbox/conditionally-rendering-a-lazy-loaded-component-only-after-the-parent-node-is-attached-causes-infinite-loop-s9gzml)

## Steps To Reproduce

1. Create a component that renders the children inside a `<div>`, but only after it has obtained reference to that div (via putting the div node into a state)
2. Pass a lazy loaded component as children

So basically something like:
```jsx
import { Suspense, lazy, useState } from 'react';

const LazyLoadedComponent = lazy(
  () =>
    new Promise((resolve) => {
      setTimeout(
        () =>
          resolve({
            default: () => <div>Lazy loaded component</div>,
          }),
        500,
      );
    }),
);

const RenderAfterMount = (props) => {
  const [node, setNode] = useState(null);

  return <div ref={setNode}>{node && props.children}</div>;
};

export const App = () => (
  <Suspense>
    <RenderAfterMount>
      <LazyLoadedComponent />
    </RenderAfterMount>
  </Suspense>
);
```

Link to code example:
https://codesandbox.io/s/vibrant-murdock-jpnznd?file=/src/App.js:542-561

## The current behavior
Runtime error due to an infinite loop.

## The expected behavior
The lazy loaded component is rendered.
