# Bug: Potential Memory Leak - Detached elements after DOM Update due to state change

> Issue #31818 - Created on 12/17/2024

> Original URL: https://github.com/facebook/react/issues/31818

## Description

React version: 18.3.1

## Steps To Reproduce

1. Create a boolean toggle
2. Show 2 different elements based on toggle
3. The element that is hidden still exists but is detached
4. Repeat to create multiple detached elements

![image](https://github.com/user-attachments/assets/d4ee6f93-7766-4e05-a43e-c73aa3869fd8)

Link to code example:
https://codesandbox.io/p/sandbox/modest-yalow-n2m86y
https://n2m86y.csb.app/

## The current behavior
Elements are never removed from memory

## The expected behavior
Elements should be removed from memory
