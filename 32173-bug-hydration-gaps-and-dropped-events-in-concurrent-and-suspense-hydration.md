# Bug: Hydration Gaps and Dropped Events in Concurrent and Suspense Hydration

> Issue #32173 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32173

## Description

<!--
 There is a delay between calling createRoot or createSyncRoot and committing the hydrated tree, leading to gaps in rendering. During these gaps, events issued on dehydrated DOM nodes are dropped. This issue is more prominent in batched and concurrent modes, where there are delays in starting the render or during yielding. For Suspense boundaries, Partial Hydration also introduces gaps between rendering levels. This problem prevents certain user events from being handled correctly until after the tree is fully hydrated.
-->

React version: 2.3.1

## Steps To Reproduce

1.Use React with Suspense boundaries or in concurrent mode.
2.Trigger events (e.g., click, text input) during the hydration gap
3.Observe that some events are not handled or are dropped.

<!--
  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hydration Gap Example</title>
  <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
</head>
<body>
  <div id="root"></div>

  <script type="text/javascript">
    const { useState, useEffect } = React;

    // Simulate a delay in rendering (such as in Concurrent Mode or Suspense boundaries)
    const DelayedComponent = () => {
      const [hydrated, setHydrated] = useState(false);

      // Simulate the hydration process
      useEffect(() => {
        setTimeout(() => {
          setHydrated(true);
        }, 3000); // Delay for 3 seconds (simulating hydration gap)
      }, []);

      // Handle a click event that will be missed during the hydration gap
      const handleClick = () => {
        alert("Button clicked!");
      };

      if (!hydrated) {
        // Show a placeholder or loading state while waiting for hydration
        return <div>Loading...</div>;
      }

      // This button will miss the first click event if clicked before hydration is done
      return (
        <div>
          <button onClick={handleClick}>Click me!</button>
        </div>
      );
    };

    const App = () => {
      return (
        <div>
          <h1>Hydration Gap Example</h1>
          <DelayedComponent />
        </div>
      );
    };

    // Initially render the component server-side (SSRed content)
    ReactDOM.hydrate(<App />, document.getElementById('root'));

    // Simulate a client-side hydration
    document.addEventListener('DOMContentLoaded', () => {
      ReactDOM.hydrate(<App />, document.getElementById('root'));
    });
  </script>
</body>
</html>



Steps to Reproduce the Bug:
Initial Render:

The page renders with the message "Loading..." and the button appears after a 3-second delay. During this period, the component is "not hydrated."
User Interaction:

If the user clicks the button before the component is hydrated (within the 3-second delay), the event will be dropped or missed because the button is still in the "dehydrated" state.
Component Hydration:

After the delay, the component becomes hydrated and ready to handle events properly. Any further clicks will work as expected.


-->

Link to code example:

<!--
  import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

// Simulate a delay in rendering (such as in Concurrent Mode or Suspense boundaries)
const DelayedComponent = () => {
  const [hydrated, setHydrated] = useState(false);

  // Simulate the hydration process
  useEffect(() => {
    setTimeout(() => {
      setHydrated(true);
    }, 3000); // Delay for 3 seconds (simulating hydration gap)
  }, []);

  // Handle a click event that will be missed during the hydration gap
  const handleClick = () => {
    alert("Button clicked!");
  };

  if (!hydrated) {
    // Show a placeholder or loading state while waiting for hydration
    return <div>Loading...</div>;
  }

  // This button will miss the first click event if clicked before hydration is done
  return (
    <div>
      <button onClick={handleClick}>Click me!</button>
    </div>
  );
};

const App = () => {
  return (
    <div>
      <h1>Hydration Gap Example</h1>
      <DelayedComponent />
    </div>
  );
};

// Initially render the component server-side (SSRed content)
ReactDOM.hydrate(<App />, document.getElementById('root'));

// For the sake of example, simulating a client-side hydration
document.addEventListener('DOMContentLoaded', () => {
  ReactDOM.hydrate(<App />, document.getElementById('root'));
});

-->

## The current behavior
Critical user interactions should be handled immediately, while less critical interactions can be replayed after hydration.

## The expected behavior
ome events are dropped due to the hydration gap, leading to a degraded user experience, especially with client-side interactions.

