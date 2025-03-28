# Bug: Wrong detection of non-boolean attribute when working with React API

> Issue #30943 - Created on 9/11/2024

> Original URL: https://github.com/facebook/react/issues/30943

## Description

I'm trying to be as concise as possible. For example, for a given `List` component, I use these boolean attributes:

```
<List
    useMenuForActions
    hasSearch
    expandable
/>
```

I see no warning in the console.

But when I write this code:

```
<td ltr>{entity.phoneNumber}</td>
```

I see this warning:

> Warning: Received `true` for a non-boolean attribute `ltr`.
> If you want to write it to the DOM, pass a string instead: ltr="true" or ltr={value.toString()}.

In both cases, I read the *boolean attribute* from `props` and act accordingly if they are present (which means they are true).
Then only difference is that for the second one (the `<td>` element) I use `React.Children` and `map` to transform them.
I checked and `ltr` is not a standard HTML attribute.

React version: 18.3.1

## Steps To Reproduce

1. Create a react project
2. Create a component with a custom boolean attribute (do anything you want with it)
3. Create a simple HTML element with a custom boolean attribute (use it in `React.Children` method to add a simple custom style for example)
4. Render both of them
5. You should see a warning for the second case

https://codesandbox.io/p/sandbox/brave-fast-5s9xxs

## The current behavior
Warning on 'ltr'

## The expected behavior
No warning should be shown
