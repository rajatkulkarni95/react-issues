# Bug: Warning: React does not recognize the `fetchPriority` prop on a DOM element [React 18.3.1]

> Issue #28948 - Created on 4/29/2024

> Original URL: https://github.com/facebook/react/issues/28948

## Description

React version: 18.3.1

This bug may be related to #28946 .

## Steps To Reproduce

1. Create an image tag with `fetchPriority="high"` attribute (camelCase)
2. Create an image tag with `fetchpriority="high"` attribute (lowercase)

Link to code example: https://codesandbox.io/p/sandbox/quiet-haze-5hkscx 

## The current behavior
**Output**: (fetchpriority attribute looks ok!)
```
<img fetchpriority="high" src="https://dummyimage.com/200x64/b000b0/fff&text=fetchPriority">
<img fetchpriority="high" src="https://dummyimage.com/200x64/00b075/fff&text=fetchpriority">
```
**Warning**: 
```
Warning: React does not recognize the `fetchPriority` prop on a DOM element. If you intentionally want it to appear in the DOM as a custom attribute, spell it as lowercase `fetchpriority` instead. If you accidentally passed it from a parent component, remove it from the DOM element.
```

## The expected behavior
The same output, but no warning.

