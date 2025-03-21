# RequestUpdateLane render phase update comment says not supported

> Issue #31633 - Created on 11/26/2024

> Original URL: https://github.com/facebook/react/issues/31633

## Description

Apologies for not following the template but this isn't a bug but also isn't about docs on react.dev - it's about a comment in the code.

While debugging a render phase setState call, I noticed `requestUpdateLane` has a comment about render phase updates not being officially supported:

https://github.com/facebook/react/blob/7670501b0dc1a97983058b5217a205b62e2094a1/packages/react-reconciler/src/ReactFiberWorkLoop.js#L673-L682

However the docs recommend using a render phase update to adjust state when props change: https://react.dev/learn/you-might-not-need-an-effect#adjusting-some-state-when-a-prop-changes

```
function List({ items }) {
  const [isReverse, setIsReverse] = useState(false);
  const [selection, setSelection] = useState(null);

  // Better: Adjust the state while rendering
  const [prevItems, setPrevItems] = useState(items);
  if (items !== prevItems) {
    setPrevItems(items);
    setSelection(null);
  }
  // ...
}
```

Is this comment out of date?
