# Bug: React use(Promise) API keeps rerendering

> Issue #32351 - Created on 2/11/2025

> Original URL: https://github.com/facebook/react/issues/32351

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0.8

## Steps To Reproduce

1. Execute code example
2. The Loading UI does not go away
3. The console.log('Fetching data...') repeats indefinitely.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
```
import { use, Suspense } from 'react';

type DataProps = { name: String; age: number };

const fetchData = async () => {
  console.log('Fetching data...');
  return new Promise<DataProps>((resolve) => {
    setTimeout(() => {
      resolve({ name: 'John Doe', age: 30 });
    }, 2000);
  });
};

const MyComponent = () => {
  const data = use<DataProps>(fetchData());
  console.log('Rendering data...');

  return (
    <div>
      <h1>{data.name}</h1>
      <p>Age: {data.age}</p>
    </div>
  );
};

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <MyComponent />
    </Suspense>
  );
}

export default App;
```
<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
The Loading UI does not go away.

## The expected behavior
The Loading UI should go away in 2 seconds.

