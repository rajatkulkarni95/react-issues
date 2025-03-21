# In react fiber, is didReceiveUpdate related to dirty checking?

> Issue #28622 - Created on 3/24/2024

> Original URL: https://github.com/facebook/react/issues/28622

## Description

https://github.com/facebook/react/blob/f09e1599d631051a559974578a6d4c06effd95eb/packages/react-reconciler/src/ReactFiberBeginWork.js#L620

I have some question while looking for ReactFiberBeginWork.js file.
**Is didReceiveUpdate related to dirty checking?**

when ```didReceiveUpdate = true``` called, it has to satisfied below conditions.
```(oldProps !== newProps || hasContextChanged() || (workInProgress.type !== current.type))```


To organize the conditions as I understand them,
1. oldProps !== newProps -> props changed
2. hasContextChanged() -> context changed
3. workInProgress.type !== current.type -> code changed

But I understand that dirty checking only works when there is a change in props. 
But didReceiveUpdate is also called for two conditions other than a change in props.
So I'm wondering if didReceiveUpdate is related to dirty checking, and if not, what's the difference

If you're not busy, it would be a great help and honor to organize and understand the concept. Thanks for your read!
