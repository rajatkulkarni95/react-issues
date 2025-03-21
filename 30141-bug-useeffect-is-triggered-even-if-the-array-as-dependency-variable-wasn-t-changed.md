# Bug: useEffect is triggered even if the array as dependency variable wasn't changed.

> Issue #30141 - Created on 6/30/2024

> Original URL: https://github.com/facebook/react/issues/30141

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: all

## Steps To Reproduce

1. Declare a state variable as array like: useState([1, 2, 3]);
2. Add a useEffect including the declared state variable in the dependency array.
3. Update the state variable with the same value.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

It might be happening because if state values are checked with '==' after using functions to set states, the comparison for arrays always returns false, triggering useEffect.

```
[1, 2, 3] == [1, 2, 3] is false:
"This condition will always return 'false' since JavaScript compares objects by reference, not value."
```

Link to code example:

```
const [arrVar, setArrVar] = useState([]);

 useEffect(() => {
    console.log("triggered");
    console.log(arrVar);
}, [arrVar])

//Click the button twice.
return (
    <button onClick={ (e) => {setArrVar([1, 2, 3])} }>update state</button>
);
```

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
useEffect is triggered even if the array element in the dependency array doesn't change when updated.

## The expected behavior
It shouldn't be triggered.

