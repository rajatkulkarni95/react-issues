# Bug: form submission validation of React textarea in Chrome

> Issue #29053 - Created on 5/14/2024

> Original URL: https://github.com/facebook/react/issues/29053

## Description

In Chrome, textareas with minimum length restriction has unexpected behavior when it is form-validated. It seems to be related to [this pull request](https://github.com/facebook/react/pull/27635).

[Here](https://plnkr.co/edit/oSBPQ2ZNvOyz44bc?open=Hello.js&deferRun=1) you have a demo (code example). Steps to reproduce:

1. Try to submit the 1st form. The browser avoids it and show you alerts.
2. Fill properly the required controls to achieve submission.
3. Then, add one letter into not-required controls and tweak them to success again. All controls must be filled and form submitted.

Repeat the same for the React-controlled (2nd) `<form>`. You will see that the last `<textarea>` fails. It has to be restricted like its sibling.

React version: 18.3.1 (latest).
