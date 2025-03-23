# React compiler healthcheck (and ESLint plugin) ignores all files if a babel.config.js file is present

> Issue #29135 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29135

## Description

## Summary

Create the following two files in a new directory:

```
// index.jsx
const App = () => <div />;

// babel.config.js
export default {};
```

Then run `npx react-compiler-healthcheck --src index.jsx`. It reports `Successfully compiled 0 out of 0 components.`

Then remove the `babel.config.js` file (or comment out the line inside it) and run `npx react-compiler-healthcheck --src index.jsx` again. It now reports `Successfully compiled 1 out of 1 components.`, as expected.

