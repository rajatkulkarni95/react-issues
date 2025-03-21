# Bug: Inaccurate Bundle Type Filtering in Rollup Build

> Issue #29614 - Created on 5/28/2024

> Original URL: https://github.com/facebook/react/issues/29614

## Description


**React version:** 18.x.x up to latest

## Steps To Reproduce

1. Clone the React repository.
2. Run: `yarn install`
3. Run either:
    - `yarn build-for-devtools-dev`
    - `yarn build-for-devtools-prod`

4. Observe the output of the `shouldSkipBundle` function logs within the `build.js` script.

## Link to code example:

* Relevant code: `scripts/rollup/build.js`
* Relevant function: `shouldSkipBundle`

## The current behavior:

The `shouldSkipBundle` function, responsible for determining whether to include a bundle in the build output, contains incorrect logic for filtering when multiple bundle types are specified.  Specifically, the following line causes the issue:

```javascript
  const isAskingForDifferentType = requestedBundleTypes.every(
    requestedType => bundleType.indexOf(requestedType) === -1
  );
```

This code uses `Array.prototype.every` with `indexOf` to check if **all** requested bundle types are missing in the current bundle type. However, when multiple types are specified, it should skip a bundle only if **none** of the requested types are present.

Here's an example of the incorrect behavior observed during debugging:

```
requestedBundleTypes [ 'NODE', 'NODE_DEV' ]
bundleType NODE_DEV
isAskingForDifferentType false

requestedBundleTypes [ 'NODE', 'NODE_DEV' ]
bundleType NODE_PROD
isAskingForDifferentType false // Incorrect behavior
```

In this case, even though the `bundleType` is `NODE_PROD` and doesn't include `NODE_DEV`, `isAskingForDifferentType` is incorrectly evaluated as `false`, leading to the bundle not being skipped.

## The expected behavior:

The `shouldSkipBundle` function should correctly filter bundles based on multiple requested types. In the example above, the expected behavior is that `isAskingForDifferentType` should be `true` for the `NODE_PROD` bundle type, as it does not include the `NODE_DEV` type.

In general, the function should return `true` (skip the bundle) only if **none** of the requested types are included in the current bundle type.

