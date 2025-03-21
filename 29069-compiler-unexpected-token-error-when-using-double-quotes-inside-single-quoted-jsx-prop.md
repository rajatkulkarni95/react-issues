# Compiler: Unexpected token error when using double quotes Inside single-quoted JSX prop

> Issue #29069 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29069

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19 RC

## Steps To Reproduce

Use double quote mark in single-quoted JSX string prop like so:

```jsx
export function Component() {
  return (<Message caption='Some "text"' />);
}
```

and you'll get this error:

![Screenshot 2024-05-15 at 20 31 15](https://github.com/facebook/react/assets/920747/4ff2c3f5-5ec9-460b-ae7c-f4c1b1e98fec)

Link to code example:

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgDMoA7OXASwhPwGEIBbbEhE3ACgEp9gAdG-DAS5YNdgB4AsgjBgAhgHME+OHMyVqAXgDkAZUbLeIXBlxHt+APQA+TgG5+AXxCOgA


