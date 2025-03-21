# Bug: React 18 freezes if state updates during unsuspended -> suspended

> Issue #29058 - Created on 5/15/2024

> Original URL: https://github.com/facebook/react/issues/29058

## Description

React version: 18.1.0

## Steps To Reproduce

Run https://stackblitz.com/edit/react-ufudqb?file=src%2FApp.js

Link to code example: https://stackblitz.com/edit/react-ufudqb?file=src%2FApp.js

### app.js
```js
import React from 'react';

function Timestamp() {
  const [now, setNow] = React.useState(Date.now());

  React.useEffect(() => {
    const timer = setInterval(
      () => {
        // when the app is frozen every update here appears to abort the render and restart it,
        // meaning the component never completes the transition from unuspended -> suspended
        setNow(Date.now());
      },
      // if you make this interval high enough then the app doesn't
      // freeze as it manages to suspend before the state update
      // interrupts it
      0
    );
    return () => clearInterval(timer);
  }, []);

  return <div>Timestamp: {now} (should not freeze)</div>;
}

const fakeLoading = new Promise((resolve) => {
  setTimeout(() => {
    fakeLoading.done = true;
    console.log('loaded');
    resolve();
  }, 5000);
});

function useRemoteData() {
  if (!fakeLoading.done) {
    // suspend!
    throw fakeLoading;
  }

  return 'the data';
}

function SomeRemoteData() {
  const data = useRemoteData();
  return <div>Data: {data}</div>;
}

function Fallback() {
  React.useEffect(() => {
    // this never happens as it appears it never manages to suspend
    console.log('===> Fallback mount');
    return () => console.log('  <=== Fallback unmount');
  });

  // ... but it is constantly attempting renders
  // console.log("Fallback render")
  return <div>Suspended: Yes</div>;
}

export default function App() {
  // Change the initial state to `true` and there is no issue
  // The problem seems to occur when going from unsuspended -> suspended,
  // and not when starting suspeneded
  const [showRemoteData, setShowRemoteData] = React.useState(false);

  React.useEffect(() => {
    setShowRemoteData(true);
  }, []);

  return (
    <div>
      <Timestamp />
      <React.Suspense
        fallback={
          // expecting to this to render when `showRemoteData` goes to `true`
          <Fallback />
        }
      >
        <div>Suspended: No</div>
        {showRemoteData && <SomeRemoteData />}
      </React.Suspense>
    </div>
  );
}
```

### index.js
```js
import React, { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

import App from './App';

const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

// strict mode disabled just to make the console logs clearer

root.render(
  // <StrictMode>
  <App />
  // </StrictMode>
);
```

## The current behavior
When the fallback should be rendered the app gets stuck in a rendering loop and the fallback is never actually mounted. You can see the timestamp stops updating.


https://github.com/facebook/react/assets/3259993/ffdd695f-45b4-4c54-a75b-76d2dec6acf4



## The expected behavior
The fallback should be rendered whilst the loading is happening, and the timestamp should keep updating.

Note this is [working in react 19](https://stackblitz.com/edit/react-9etgvl?file=src%2FApp.js) 🎉 but would be great to get a patch for 18 in the meantime.

Also this may be related to #27161

Thanks
