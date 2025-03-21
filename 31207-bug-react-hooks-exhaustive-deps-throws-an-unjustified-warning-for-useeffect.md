# Bug: react-hooks/exhaustive-deps - throws an unjustified warning for useEffect

> Issue #31207 - Created on 10/13/2024

> Original URL: https://github.com/facebook/react/issues/31207

## Description

A fairly simple and straightforward code sample is causing a warning. I might be wrong, and I apologize if that's the case, but this seems like a bug on your end.

**React Hook useEffect received a function whose dependencies are unknown. Pass an inline function instead** 

React version: ^18.2.0

## Steps To Reproduce

1. Run lint on the code below.

```
const foo = { bar: () => console.log('Do something once at component mount') }

export default memo(function Example () {
  useEffect(foo.bar, [])
  return <div />
})
```
As you might guess, there is a function that should be triggered once when the component mounts. It returns undefined...

## The current behavior
Throws the warning:  **React Hook useEffect received a function whose dependencies are unknown. Pass an inline function instead** 

## The expected behavior
Not to throw

