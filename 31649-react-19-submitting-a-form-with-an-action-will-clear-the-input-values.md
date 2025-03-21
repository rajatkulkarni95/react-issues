# [React 19] Submitting a `<form>` with an `action` will clear the input values

> Issue #31649 - Created on 11/30/2024

> Original URL: https://github.com/facebook/react/issues/31649

## Description

## Summary

I think a regression was introduced during the development of React 19 Canary.

### Steps to reproduce

Render the following form and type something into the "query" input.

```jsx
<form action={() => {}}>
  <input name="query" />
  <button type="submit">Search</button>
</form>
```
 - up until `19.0.0-canary-4c12339ce-20240408`, submitting the form will preserve the input value
 - from `19.0.0-canary-adb717393-20240411` onwards, submitting the form will clear the input value

https://codesandbox.io/p/sandbox/elastic-merkle-yykcrc

### Why I think this is a bug

Clearing inputs can be problematic if we keep displaying the form after submission.

A classical example is the display of validation errors after a rejected submit (by using the information returned by [`useActionState`](https://react.dev/reference/react/useActionState#using-information-returned-by-a-form-action), for instance). If the inputs are cleared after submit, the errors would show up under empty inputs, which is not very helpful. Also, the user would have to fill in the complete form again, instead of simply fixing invalid values.
