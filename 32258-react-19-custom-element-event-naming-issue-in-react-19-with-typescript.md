# [React 19] Custom element event naming issue in React 19 with TypeScript

> Issue #32258 - Created on 1/29/2025

> Original URL: https://github.com/facebook/react/issues/32258

## Description

## Summary

Hi React team,

First off, thank you for making custom elements fully compatible with React 19! It’s been a great experience writing less code while leveraging custom elements. 

I came across an issue when using a custom element with events in a React TSX file (as shown in the picture below). TypeScript throws an error when the event name doesn’t contain a hyphen (-). However, based on the test cases [here](https://github.com/facebook/react/pull/22184), it looks like event names should be valid as long as they follow the `on-` prefix.

![Image](https://github.com/user-attachments/assets/3eaae2f7-3971-4b6d-91d8-c33252d1d0ad)

Would love to hear your thoughts on this—happy to provide more details if needed!

Repository: https://github.com/wsuwt/react-v19-ts-custom-element



