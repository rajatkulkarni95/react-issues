# Bug: Parent rerenders unnecessarily on Child-to-Parent setter call, while child rerenders only when changes occur.

> Issue #28287 - Created on 2/9/2024

> Original URL: https://github.com/facebook/react/issues/28287

## Description

React version: 18

## Steps To Reproduce

1. Define state in the parent component.
```typescript
const [state, setState] = useState();
```
2. Render the child component and pass the function to modify the parent component's state to the child component.
```html
<ChildComponent setState={setState} />
```
3. Calls the setter but does not change the value of state.
```typescript
setState((state) => state + 0);
```

Link to code example: https://codesandbox.io/p/sandbox/rendering-test-vts4v2?file=%2Fsrc%2FApp.js%3A3%2C20

## The current behavior
The parent component rerenders even if the state remains unchanged.
When the parent component rerenders only due to unchanged state, the child component does not rerender.
![image](https://github.com/facebook/react/assets/87481129/be7d453b-595c-4509-a2af-c7a81b608058)

If the value of state has been changed, the child components are rerendered.
![image](https://github.com/facebook/react/assets/87481129/28268d31-d080-4db2-a69e-8346819701be)

## The expected behavior
The parent component should not rerender if the state remains unchanged.
If the parent component rerenders, the child component should also rerender.
