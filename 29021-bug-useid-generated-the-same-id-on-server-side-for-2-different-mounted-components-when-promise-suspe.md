# Bug: useId generated the same ID on server-side for 2 different mounted components when Promise/Suspense is involved

> Issue #29021 - Created on 5/8/2024

> Original URL: https://github.com/facebook/react/issues/29021

## Description

React version: 18.3.1

_(Also tested on React 19 and seems like it is fixed)_

## Steps To Reproduce

1. Create 2 components: Parent and Child, where both components will throw Promise (eg. data fetching)
2. Call `useId` on both Parent and Child, and observes they have the same ID generated

Sample code:

```tsx
const Child = ({ parentId }: { parentId: string }) => {
  const id = useId();
  useAsync(2); // Just assume it is a hook that will throw Promise in first call
  return (
    <ul>
      <li>Parent: {parentId}</li>
      <li>Child: {id}</li>
    </ul>
  );
};

const Parent = () => {
  const id = useId();
  useAsync(1); // Just assume it is a hook that will throw Promise in first call
  return <Child parentId={id} />;
};
```

Generated HTML:

```html
<ul>
  <li>Parent: <!-- -->:R0:</li>
  <li>Child: <!-- -->:R0:</li>
</ul>
```

Link to code example: https://codesandbox.io/p/sandbox/react-server-duplicate-useid-nllf55

## The current behavior

The ID generated on both mounted components are the same

```html
<ul>
  <li>Parent: <!-- -->:R0:</li>
  <li>Child: <!-- -->:R0:</li>
</ul>
```

## The expected behavior

The ID generated on both mounted components should be different

```html
<ul>
  <li>Parent: <!-- -->:R0:</li>
  <li>Child: <!-- -->:R1:</li>
</ul>
```
