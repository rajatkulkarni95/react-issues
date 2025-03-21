# Nested <form> elements error with "A React form was unexpectedly submitted."

> Issue #28435 - Created on 2/24/2024

> Original URL: https://github.com/facebook/react/issues/28435

## Description

## Overview
Nested form elements are invalid HTML and cause a hydration error, falling back to client-rendering. When we client render, we add back the nested <form> element, but when you submit the form we error with a cryptic:

> A React form was unexpectedly submitted. If you called form.submit() manually, consider using form.requestSubmit() instead. If you're trying to use event.stopPropagation() in a submit event handler, consider also calling event.preventDefault().

Instead, we should error saying that nested form elements are invalid HTML even after (on only with) client render. We could also match the browser behavior of ignoring the nested form element and submitting the parent form action.

There is an earlier warning about the invalid form elements:

> Warning: validateDOMNesting(...): <form> cannot appear as a descendant of <form>.

React version: canary

## Steps To Reproduce

https://codesandbox.io/p/sandbox/friendly-paper-8frfc9

