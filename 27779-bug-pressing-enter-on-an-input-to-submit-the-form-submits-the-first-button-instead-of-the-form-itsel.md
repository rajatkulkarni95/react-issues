# Bug: Pressing `enter` on an input to submit the form submits the first button instead of the form itself (With Actions)

> Issue #27779 - Created on 12/3/2023

> Original URL: https://github.com/facebook/react/issues/27779

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: `18.3.0-canary-6db7f4209-20231021` in the sandbox, also works on `18.2.0`

## Steps To Reproduce

1. Create a form with one input and two buttons.
2. Add an action to the form, and a different action to the first of the two buttons. Make sure they do something different (like give out different alerts).
3. Write something in the input and press `enter`.
4. The first button's action (which was different from the form's main action) will be called, instead of the forms action being called.
5. Alternatively, look at the sandbox below.

Link to code example: https://codesandbox.io/p/sandbox/react-form-input-enter-action-demo-kd7qgr

This sandbox was forked from a [sandbox](https://codesandbox.io/s/dsnkwm?file=%2FApp.js) that was [directly in the documentation](https://react.dev/reference/react-dom/components/form#handling-multiple-submission-types). It was changed to make the textarea an input.

## The current behavior

When typing something into the input and pressing enter to submit the form, the first button's submit handler gets called, which runs the `formAction` of the button (if present, otherwise it runs the `action` of the form). You can test this out by using the two forms in the sandbox. The first one has the button without a separate action placed first in the DOM, and the second has the one with the separate action placed first in the DOM.

## The expected behavior

When pressing `enter` on the input, it should run the action of the form itself, and not of some button. There will be no way to run the correct action without putting a button without an action first in line, but this is unintuitive.

## Suggestions

Please make it so that when enter is pressed on any input in the form, it runs the form's main action, or maybe there can be support added for the input to have its own `formAction` without it being a `type='submit'` input, and that action gets called when the form is submitted.

## Temporary fix

The temporary fix is to add a button with `display: none` and `type="submit"` before any button with a custom action. This ensures that the main form's action is run.

Thank you.

