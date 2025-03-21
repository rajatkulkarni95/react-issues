# Bug: Removal of custom element property sets it to `null` rather than `undefined`

> Issue #28203 - Created on 2/2/2024

> Original URL: https://github.com/facebook/react/issues/28203

## Description

React version: experimental

## Steps To Reproduce

1. Set up a React project with `react@experimental` & `react-dom@experimental` which includes custom element property support.
2. Render a custom element with a property value provided as prop, then on a re-render remove that prop.

e.g.

```jsx
function App() {
  const [condition, setCondition] = useState(false);
  return (
    <>
      <button onClick={() => setCondition(c => !c)}>toggle</button>
      {condition ? <my-element foo={"foo"} /> : <my-element />}
    </>
  );
}
```

Link to code example:
https://stackblitz.com/edit/vitejs-vite-dz2rka?file=src%2FApp.tsx

## The current behavior

The value of the `foo` property on `<my-element>` will start off `undefined`. Toggling condition to `true` will set the property to `"foo"`, but subsequently toggling condition back to `false` will set the property to `null`.

## The expected behavior

I would expect the property to be `undefined`.

