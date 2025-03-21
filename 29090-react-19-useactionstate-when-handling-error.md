# [React 19] useActionState when handling error

> Issue #29090 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29090

## Description

## Summary

https://react.dev/reference/react/useActionState

```javascript
const [state, action] = useActionState(reduce, initState)
return <button type="button" onClick={action}>hit me!</button>
```

It looks like the docs are assuming that the `reduce` parameter function never throws an error or returns a rejected promise.

After some play with the api, I got the following behaviour, if `reduce` throws an error or returns a rejected promise:

- The error is propagated to the upper parent and the react tree collapses.
- There is no way to stop the propagation outside the call, i.e., `action().catch(console.error)` does not prevent the react tree from collapsing.

My question is that: is this expected behavior?

If yes, this mean, everytime I use `useActionState` I have to add `try/catch`. Previously, with onClick, I didn't have to do this, uncaught error in onClick does not collapse the react tree.

----

### Second issue
This is rather a suggestion to improve the docs.

Currently, the docs are sticking `useActionState` with the usage in a form, which confuses readers (like me), because form usage (via `action` props) and `useActionState` are independent. Separating the form integration to a subsection would be easy to follow the docs.

`useActionState` is also exported from `react`, not `react-dom`.

For example:

#### current docs

useActionState returns an array with exactly two values:

- The current state. During the first render, it will match the initialState you have passed. After the action is invoked, it will match the value returned by the action.
- A new action that you can pass as the action prop to your form component or formAction prop to any button component within the form.


#### Can be change to

useActionState returns an array with exactly two values:

- The current state. During the first render, it will match the initialState you have passed. After the action is invoked, it will match the value returned by the action.
- A new action that is a function accepting a single argument. When this action is called, it will call the `action` function passed as the second parameter of `useActionState`.

By the way, somehow I feel like `useActionState = useReducer + useTransition + async support`, hence the name `useAsyncReducer`?


#### isPending

It seems that `useActionState` return an array with three elements. The last element isPending, this is not mentioned in the docs.

https://webdeveloper.beehiiv.com/p/react-19-beta-release-quick-guide
