# Bug: useEffect Hook Does Not Recognize Passed Prop as Function in Child Component

> Issue #28144 - Created on 1/29/2024

> Original URL: https://github.com/facebook/react/issues/28144

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18 or higher

## Steps To Reproduce
Expected Behavior:
The useEffect hook in the child component should recognize and execute the setIsRendered function passed from the parent component as a prop without any errors.

Current Behavior:
When attempting to invoke the setIsRendered function, which is passed as a prop from the parent component to the child component and used inside a useEffect hook, the application throws an error stating "setIsRendered is not a function".

Steps to Reproduce:

Define a state isRendered and its setter setIsRendered in the parent component using useState.
Pass setIsRendered to the child component as a prop.
In the child component, attempt to call setIsRendered(true) within a useEffect hook with an empty dependency array.
Observe the error in the console upon component mounting.

```
// Code Snippet (Parent Component):
const ParentComponent = () => {
  const [isRendered, setIsRendered] = useState(false);

  return <ChildComponent setIsRendered={setIsRendered} />;
};


// Code Snippet (Child Component):
const ChildComponent = ({ setIsRendered }) => {
  useEffect(() => {
    setIsRendered(true);
  }, []);

  return <div>Child Content</div>;
};
```


