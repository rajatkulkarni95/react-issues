# Bug: unstable_runWithPriority continious loop

> Issue #28470 - Created on 2/29/2024

> Original URL: https://github.com/facebook/react/issues/28470

## Description

React version:
16.12.0
## Steps To Reproduce

1. add a flushSync() to the HOC-styled component
```javascript
import React from 'react'
import { useState, useEffect } from 'react';
import { flushSync } from 'react-dom';

export default function printMedia(WrappedComponent) {
  return (props) => {
    const [isPrinting, setIsPrinting] = useState(false);
    useEffect(() => {
    function handleBeforePrint() {
      flushSync(() => {
        setIsPrinting(true);
      })
    }

    function handleAfterPrint() {
      setIsPrinting(false);
    }

    window.addEventListener('beforeprint', handleBeforePrint);
    window.addEventListener('afterprint', handleAfterPrint);
    return () => {
      window.removeEventListener('beforeprint', handleBeforePrint);
      window.removeEventListener('afterprint', handleAfterPrint);
    }
  }, []);

  return (
    <>
      <h1>isPrinting: {isPrinting ? 'yes' : 'no'}</h1>
      <button onClick={() => window.print()}>
        Print
      </button>
    </>
  )}};
``` 

2. execute window.print()

## The current behavior

continious loop on  function:
unstable_runWithPriority(priorityLevel, eventHandler)

## The expected behavior
working

