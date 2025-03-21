# Bug:  Manually added event listener always triggered

> Issue #28742 - Created on 4/4/2024

> Original URL: https://github.com/facebook/react/issues/28742

## Description


React version:  18.0.0

## Steps To Reproduce

1. open the sandbox link.
2. open console.
3. click on the child text you can see on console there is two log manually added listener and also the react synthetic event.

Link to code example:

https://codesandbox.io/p/sandbox/event-bubble-m7x98y


## The current behavior
It always triggers both event if I click on the child text, it triggers manually added parent eventlistener. It should only trigger the onPointerDown event not the parent. I tried to stop the event bubbling using event.stopPropagation() still no success.

Also tried using

```
new Event("pointerdown",{
bubbles:false,
}) 
```

but the event is not emitted to child.




## The expected behavior

If i click on the child text it should only trigger its onPointerDown event not the parent event.



