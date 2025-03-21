# Bug: JSX <title> won't work if the HTML already has a static <title> markup

> Issue #29031 - Created on 5/9/2024

> Original URL: https://github.com/facebook/react/issues/29031

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:

## Steps To Reproduce

1. Create a new React app
2. Insert `<title>Foobar</title>` into `index.html`
3. Insert `<title>Hello World</title>` into `App.tsx`

Link to code example:

Code https://codesandbox.io/p/sandbox/test-title-r736t9

Preview https://r736t9.csb.app/

## The current behavior
`Foobar` is shown as title

## The expected behavior
`Hello Wolrd` should be the title
