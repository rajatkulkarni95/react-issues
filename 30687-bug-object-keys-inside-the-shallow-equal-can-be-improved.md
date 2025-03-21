# Bug: Object.keys inside the Shallow Equal can be improved 

> Issue #30687 - Created on 8/14/2024

> Original URL: https://github.com/facebook/react/issues/30687

## Description

if we look at this file https://github.com/facebook/react/blob/main/packages/shared/shallowEqual.js
which is a utility for shallowEqual, in this code we are using Object.keys() method,  i tried to have this method working without Object.keys() , which does not create intermediate arrays.

this actually has a near around 30% better performance in the comparison loop we are trying to do, now that can be something that varies from browser to browser, and also due to many other factors, but would love to know the opinion of the maintainers of the same of what they think about, i am attaching a JS benchmark which calculates the benchmark for the both piece of code.



React version: 18.2.0

## Steps To Reproduce

1. check the JS benchmark https://jsben.ch/d9SVb
2. click on run tests

The code block 2 contains the piece of code which does not uses Object.keys() and is much faster.




https://github.com/user-attachments/assets/8fbe9850-8f4d-4de4-be15-96bff5db10dd





**Current Code**

```
function shallowEqual(objA, objB) {
  if (is(objA, objB)) {
    return true;
  }

  if (
    typeof objA !== 'object' ||
    objA === null ||
    typeof objB !== 'object' ||
    objB === null
  ) {
    return false;
  }

  const keysA = Object.keys(objA);
  const keysB = Object.keys(objB);

  if (keysA.length !== keysB.length) {
    return false;
  }

  // Test for A's keys different from B.
  for (let i = 0; i < keysA.length; i++) {
    const currentKey = keysA[i];
    if (
      !hasOwnProperty.call(objB, currentKey) ||
      !is(objA[currentKey], objB[currentKey])
    ) {
      return false;
    }
  }

  return true;
}
for(let i = 0; i <= 1000; i++){

shallowEqual(a, b);
}

```

**Code that has a  better performance**

```
function shallowEqual(objA, objB) {
  if (is(objA, objB)) {
    return true;
  }

  if (
    typeof objA !== 'object' ||
    objA === null ||
    typeof objB !== 'object' ||
    objB === null
  ) {
    return false;
  }
 let aLength = 0;
  let bLength = 0;

  for (const key in objA) {
    aLength += 1;

    if (!hasOwnProperty.call(objB, key) || !is(objA[key], objB[key])) {
      return false;
    }
  }

  for (const _ in objB) {
    bLength += 1;
  }

  return aLength === bLength;
}
 for(let i = 0; i <= 1000; i++){
shallowEqual(a, b);
 }


```

