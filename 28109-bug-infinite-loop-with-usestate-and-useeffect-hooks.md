# Bug: Infinite loop with useState and useEffect hooks

> Issue #28109 - Created on 1/26/2024

> Original URL: https://github.com/facebook/react/issues/28109

## Description

I am using default pattern for updating state if props changes.

React version: 18.2.0

## Steps To Reproduce

1. Create component with useState and useEffect and some prop with array
2. Update state value on prop changes in useEffect
3. Add default value for prop as empty array
4. Do not pass value via prop in the component

Link to code example: [https://codesandbox.io/p/sandbox/beautiful-http-n4c3p5](https://codesandbox.io/p/sandbox/beautiful-http-n4c3p5)

```jsx
export default function App() {
  return (
    <div className="App">
       <List />
    </div>
  );
}
```

```jsx
export function List({ items = [] }) {
  const [itemsState, setItemState] = useState([]);

  useEffect(() => {
    setItemState(items); // this line starts infinite loop
  }, [items]);

  return <div>Length: {itemsState.length}</div>;
}
```

## The current behavior
infinite loop

## The expected behavior
set value to state if prop `items` changes

