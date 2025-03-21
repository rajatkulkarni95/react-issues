# [React 19] `form.requestSubmit()` resets input value/defaultValue after transition

> Issue #30532 - Created on 7/30/2024

> Original URL: https://github.com/facebook/react/issues/30532

## Description

## Summary

When form is submitted through `form.requestSubmit()` the input displays the older value instead of the current state.

https://github.com/user-attachments/assets/37bcbaaf-b680-43f0-95db-a57d276753a1

I tested using `value` and `defaultValue` props, and both leads to the same issue. When the form is submitted through `<button type="submit">` it works fine, and `form.submit()` also has no problem, the issue is only using `form.requestSubmit()`.
I suspect that this is an issue in `react-dom` reconciler. The state is correct in the log, but the actual `<input>` value is not.
In the repro there is an `useOptimistic` but this happens without it too.

Repro: https://stackblitz.com/edit/vitejs-vite-i9sbuj?file=src%2FApp.tsx

Version:
```
"react": "^19.0.0-rc-941e1b4a-20240729",
"react-dom": "^19.0.0-rc-941e1b4a-20240729"
```

> To make sure this wasn't reported, I tried searching for `transition state reset`, `useActionState` and `requestSubmit`, didn't find anything related.

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

