# Bug: When input type=number, input 1-1 cannot trigger an onchange and cannot be set to an empty string

> Issue #30459 - Created on 7/25/2024

> Original URL: https://github.com/facebook/react/issues/30459

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: all

## Steps To Reproduce

1. Input 1-1
2. Set the value to an empty string

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
```
const Test = () => {
    const [value, setValue] = useState('')

    return <input type="number" value={value} onChange={e => {
        console.log(e.target.value)
        if (e.target.value === '') {
                // Triggered when inputting 1-
                setValue('')
        } else {
                setValue(e.target.value)
        }
    }} />
}
```

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
1. Input 1-1 will not trigger an onchange
2. setValue ('') will not reset 1-
3. This seems to be a browser bug

## The expected behavior
1. Input 1-1 to trigger onchange
2. setValue ('') reset 1-

