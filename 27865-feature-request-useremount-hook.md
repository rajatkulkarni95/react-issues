# Feature Request: `useRemount()` hook

> Issue #27865 - Created on 1/1/2024

> Original URL: https://github.com/facebook/react/issues/27865

## Description

I would like to propose a new hook, `useRemount` which allows the current component to be remounted, causing all state, etc to be reset.

Usage:
```tsx
function exampleComponent() {
    const remount = useRemount();

    return <button onClick={remount} />
}
```

This is a "low-level" hook that would typically be used by higher level wrappers like the following custom hook:
```tsx
function useKey(key: any) {
    const remount = useRemount();
    useEffect(() => () => {
        remount();
    }, [key])
}

function exampleComponentWithIdProp({itemId}, {itemId: string}) {
    useKey(itemId);
    const [editedValue, setEditedValue] = useState(null);

    ...
}
```

This pattern is a much safer way to prevent the "editedValue" from being transferred between items with different IDs, compared to the current solution where the parent component has to remember to pass in the `key` prop.

A similar use-case is for modals. It is a common pattern for a modal to take an `isOpen` prop so that the parent can determine when to open the modal. However, this can lead to the modal state not being properly reset between openings.

```tsx
function modalComponent({isOpen}: {isOpen: boolean}) {
    useKey(isOpen);
    const [value, setValue] = useState("");

    ...
}
```

The remount functionality allows the modal to easily reset its own state as required.
