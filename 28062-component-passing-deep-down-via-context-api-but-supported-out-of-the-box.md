# Component passing deep down via context api but supported out of the box

> Issue #28062 - Created on 1/24/2024

> Original URL: https://github.com/facebook/react/issues/28062

## Description

Hi/ Namaste

In certain scenarios, it becomes necessary to have custom components rendered instead of the given one (say via 3rd party libraries). An example can be an existing library rendering some input component, but we want our custom component to be rendered. So, an example can be:
```jsx
import Component from 'some-3rd-party-library';

<div>
    <Component />
</div>

```
This component may contain child components and so on, finally leading to render an input like:
```jsx
function Some_Child_Component_In_Hierarchy() {
    return ....
    ...
        <input type="text"/>
    ...;
}

```
Now, one way to have some custom component is to pass some prop via context api and let the `Some_Child_Component_In_Hierarchy` decide the appropriate component to render, Or even pass the component via the context api.

But what if the `Some_Child_Component_In_Hierarchy` is a third party who have fixed the input component and we have no way to pass the info?
In our custom implementations, we can alter the way we wish, but especially in the above case, it is impossible to do.

So, one solution I can think of is to:
1. Provide the component via context api.
One possible implementation:

```jsx
export type ComponentContextType = Record<any, any>;

export const ComponentContext = React.createContext<ComponentContextType>({});

export const ComponentProvider = ComponentContext.Provider;

export function Override(props: Record<string, any>) {
    // eslint-disable-next-line react/prop-types
    const { children, ...other } = props;
    return <ComponentProvider value={other}>{children}</ComponentProvider>;
}
```
Now, any component can provide Override for child components via:
```jsx
<Override h1={My_Custom_H1} TextField={My_Custom_Field} (... other overrides as desired)>
    <Component />
</Override>
```
2. React.createElement (or jsx or jsxs etc.) will determine which component to render. One possibility is to by default wrap every component to another component viz:
```jsx
function new_Jsx(elt, props) {
    const newProps = { Orig: elt, props };
    return original_Jsx(OverridenOrOriginal, newProps);
}

function OverridenOrOriginal({ Orig, props }) {
    const { name } = Orig; // In case of Custom component, we have name else Orig is a string
    const { [name ?? Orig]: Overriden } = useContext(ComponentContext); // We may create a custom hook for this
    if (Overriden) {
        return original_Jsx(Overriden, props);
    } else {
        return original_Jsx(Orig, props);
    }
}
```
Well, this can be achieved while making our own components but I am proposing here to make it universal. Please let me know your thoughts.

Thanks & Regards,
Praveen
