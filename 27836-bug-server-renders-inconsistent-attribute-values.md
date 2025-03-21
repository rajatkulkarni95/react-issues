# Bug: Server renders inconsistent attribute values

> Issue #27836 - Created on 12/15/2023

> Original URL: https://github.com/facebook/react/issues/27836

## Description

- https://github.com/vercel/next.js/issues/47617
- https://github.com/facebook/react/pull/22041

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: v18.1.0

## Steps To Reproduce
```tsx
import React from 'react';
import { renderToString } from 'react-dom/server';

console.log(renderToString(<div class="mt:0>div"></div>))
```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://stackblitz.com/edit/react-zvjacx?file=src%2FApp.js,src%2Findex.js

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
`renderToString` or `renderToStaticMarkup` have the same problem.
```tsx
import React from 'react';
import { renderToString } from 'react-dom/server';

renderToString(<div class="mt:0>div"></div>)
// ❌ <div class="mt:0&gt;div"></div>
```

## The expected behavior
```tsx
import React from 'react';
import { renderToString } from 'react-dom/server';

renderToString(<div class="mt:0>div"></div>)
// ✅ <div class="mt:0>div"></div>
```
React should not encode the entire string, especially in class and CSS-related string processing, which will cause the CSS selector to be selected incorrectly.

`mt:0>div` is a valid class syntax for [Master CSS](https://css.master.co).
