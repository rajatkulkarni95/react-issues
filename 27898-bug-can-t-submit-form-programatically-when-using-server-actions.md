# Bug: Can't submit form programatically when using server actions

> Issue #27898 - Created on 1/8/2024

> Original URL: https://github.com/facebook/react/issues/27898

## Description

I'm using Server Actions and I'm trying to do some stuff before submitting the form so I added the following handler that does some stuff then submits the form
```js
export const handleFormWithRecaptcha = (action: string) => {
    return (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();
        // Some stuff
        e.target.submit()
    }
}
```
But the code above throws the following error
```
Uncaught Error: A React form was unexpectedly submitted. If you called form.submit() manually, consider using form.requestSubmit() instead. If you're trying to use event.stopPropagation() in a submit event handler, consider also calling event.preventDefault().
    at <anonymous>:1:7
```
Following the error suggestion actually results in an infinite loop since I'm requesting a submit within the onSubmit handler itself. I think there should be better error messages
anyway, shouldn't I be able to just call form.submit?


React version: Whatever version Next 14.0.4 is using

## Steps To Reproduce

1. Create a form with a server action
2. Add an obSubmit handler that does some stuff then submits the form programtically


