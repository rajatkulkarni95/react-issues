# Bug: `use()` Delays Loading in Unrelated Components, Suspense Waits for Unrelated `use()` Calls

> Issue #28070 - Created on 1/24/2024

> Original URL: https://github.com/facebook/react/issues/28070

## Description

React version: experimental (0.0.0-experimental-e1d20fc0c-20240122)

## Steps To Reproduce

Link to code example: https://codesandbox.io/p/sandbox/react-use-repro-jq8zqs

To reproduce the issue, render multiple components as siblings within a React application. Each component includes a Suspense boundary and uses the `use()` hook for data loading. There are two types of components involved:

- `UseExampleSequential`, which loads data sequentially within `use()`, and
- `UseExampleParallel`, which loads data in parallel via props as recommended in the React documentation (https://react.dev/reference/react/use#resolve-promise-in-server-or-client-component).

Each component loads data two times from a fake API with different arguments. Each fake API call takes 1 second to complete. So the parallel loading components should render after 1 second, and the sequential loading components should render after 2 seconds.

The data loading is cached:

```js
async function doFakeFetch(data) {
  // wait 1 second so that we can see the loading state
  await new Promise((resolve) => setTimeout(resolve, 1000));
  return "loaded - " + data;
}

const cache = new Map();
export function loadData(data) {
  if (!cache.has(data)) {
    cache.set(data, doFakeFetch(data));
  }
  return cache.get(data);
}
```

## The current behavior

Currently, only the first child component (`UseExampleParallel`) displays after 1 second. All other children components delay their rendering until all promises are resolved, leading to a total rendering time of about 5 seconds for all components. Consequently, the entire application ends up rendering after about 5 seconds, regardless of the mix of parallel and sequential components.


## The expected behavior

In the expected scenario, each `UseExampleParallel` component should render after approximately 1 second, and each `UseExampleSequential` component should render after approximately 2 seconds. Overall, the complete application is expected to render after roughly 2 seconds.

## Further Information

Observations show that when only parallel components are used, the app's loading time remains around 1 second. However, with the addition of sequential components, each additional component increases the app's loading time by 1 second. 

Additionally, parallel loading components (other than the first child) also wait for sequential components to finish loading before displaying their content.

It seems to me, that the problem only appears, if data is loaded in a component which is inside a Suspense boundary. If the data is loaded outside the Suspense boundary and passed as props to the component, the problem does not appear.

