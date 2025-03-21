# Bug: useCallback doesn't work sometimes inside memo component

> Issue #29696 - Created on 6/1/2024

> Original URL: https://github.com/facebook/react/issues/29696

## Description

**React: 18.3.1**

In the following snippet (taken from React documentation), the console.log prints always false because each time the component rerendered, useCallback returns a new function reference: (only when the component is nested inside ProductPage component, but if I put ShippingForm directly under App component useCallback  works fine)


```
let lastFakeFn = null;

const ShippingForm = memo(({ onSubmit }) => {
    const [count, setCount] = useState(1);

    const fakeFn = useCallback(() => {

    }, []);
    console.log(lastFakeFn === fakeFn)
    lastFakeFn = fakeFn;

    return (
            <label>
                Number of items:
                <button type="button" onClick={() => setCount(count - 1)}>–</button>
                {count}
                <button type="button" onClick={() => setCount(count + 1)}>+</button>
            </label>
    );
});
```
