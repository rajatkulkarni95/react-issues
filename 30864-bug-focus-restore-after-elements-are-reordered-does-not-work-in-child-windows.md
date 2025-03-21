# Bug: Focus restore after elements are reordered does not work in child windows

> Issue #30864 - Created on 9/3/2024

> Original URL: https://github.com/facebook/react/issues/30864

## Description

This affects various Microsoft products that use child windows, and is an accessibility bug for users because focus is lost when they interact with an app and the active element is moved in DOM by React.

React version: 18.3.1

## Steps To Reproduce

1. Clone the repro repo https://github.com/ling1726/react-child-window-focus-repro
2. Run `npm install`
3. Run `npm run dev`
4. Open the demo app in `http://localhost:5173/`
5. Reorder the items with `ArrowUp` and `ArrowDown`
6. Open example in child window
7. Reorder the items with `ArrowUp` and `ArrowDown`
8. Notice that focus is lost immediately after reordering

Recording: 
![focus repro](https://github.com/user-attachments/assets/81c4b4f9-08b5-4356-8251-49b909771f3f)

Link to code example: https://github.com/ling1726/react-child-window-focus-repro


## The current behavior
The current `getActiveElementDeep` always uses the global `window` keyword. **Note this snippet is from the React codebase**
https://github.com/facebook/react/blob/4f604941569d2e8947ce1460a0b2997e835f37b9/packages/react-dom-bindings/src/client/ReactInputSelection.js#L59-L71

This fails focus restore when the active element is moved by React because it never gets the correct active element in a child window. 

## The expected behavior

When React moves an active element it should restore focus to the active element in a child window
