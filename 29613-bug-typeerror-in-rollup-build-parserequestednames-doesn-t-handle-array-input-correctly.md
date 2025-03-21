# Bug: TypeError in Rollup build: parseRequestedNames doesn't handle array input correctly

> Issue #29613 - Created on 5/28/2024

> Original URL: https://github.com/facebook/react/issues/29613

## Description

<!--
Please provide a clear and concise description of what the bug is. Include
screenshots if needed. Please test using the latest version of the relevant
React packages to make sure your issue has not already been fixed.
-->

React version: 18.x.x up to latest
Node version: 16.x.x up to latest

## Steps To Reproduce

1. Clone the React repository.
2. Run: `yarn install`
3. Run either:
    - `yarn build-for-devtools-dev`
    - `yarn build-for-devtools-prod`

**Link to code example:**

- Relevant code: `scripts/rollup/build.js` (line 72)
- Relevant function: `parseRequestedNames`

**The current behavior:**

https://github.com/facebook/react/assets/111031253/80d3b45c-d93d-4ffe-a801-c4494582f14f

When running the commands `yarn build-for-devtools-dev` or `yarn build-for-devtools-prod`, a `TypeError` is thrown: `names[i].split is not a function`. This is evident in the provided screenshot. The error originates from the `parseRequestedNames` function in `scripts/rollup/build.js`.

The problem stems from how the `argv.type` value is handled. In these specific commands, `argv.type` is passed as an array (e.g., `['NODE', 'NODE_DEV']`), but the code incorrectly wraps it in another array:

```jsx
const requestedBundleTypes = argv.type
  ? parseRequestedNames([argv.type], 'uppercase') // Incorrect wrapping
  : [];

```

The `parseRequestedNames` function then attempts to apply the `.split(',')` method to each element of `names`, expecting them to be strings. However, due to the erroneous wrapping, it encounters an array instead, leading to the TypeError.

```jsx
function parseRequestedNames(names, toCase) {
  let result = [];
  for (let i = 0; i < names.length; i++) {
    let splitNames = names[i].split(',');
    for (let j = 0; j < splitNames.length; j++) {
      let name = splitNames[j].trim();
      if (!name) {
        continue;
      }
      if (toCase === 'uppercase') {
        name = name.toUpperCase();
      } else if (toCase === 'lowercase') {
        name = name.toLowerCase();
      }
      result.push(name);
    }
  }
  return result;
}

```

**The expected behavior:**

The `yarn build-for-devtools-dev` or `yarn build-for-devtools-prod` commands should run without errors. The `argv.type` value should be handled correctly even when passed as an array, and bundle type filtering should work as expected.

**Additional information:**

- The `yarn build` or `yarn build-for-devtools` commands work without issues because the `argv.type` value is passed as a string or undefined.
- The `parseRequestedNames` function generates `requestedBundleTypes` and `requestedBundleNames` arrays based on the provided names (`argv.type` or `argv._`). These arrays are used for bundle filtering in the `shouldSkipBundle` function.
