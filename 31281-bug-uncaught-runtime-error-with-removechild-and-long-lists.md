# Bug: Uncaught runtime error with 'removeChild' and long lists

> Issue #31281 - Created on 10/17/2024

> Original URL: https://github.com/facebook/react/issues/31281

## Description

React version: 18.3.1

## Steps To Reproduce

1. `$ npx create-react-app my-app`
2. `$ cd my-app`
3. Replace the contents of App.js with the code listed below
4. `$ npm run start`
5. Open the page in Google Chrome or Edge (issue does not reproduce in Firefox/Safari)
6. Click one of the "x" labels
7. Click "hide"

```js
// App.js
import { useState } from 'react';

function App() {
  const [show, setShow] = useState(false);
  return (
    <div>
      {Array(950).fill().map(() => <span onClick={() => setShow(true)} key={`rng_${Math.random()}`}>x</span>)}
      <div>
        {show && (
          <div>
            <button onClick={() => setShow(false)}>Hide</button>
          </div>
        )}
      </div>
    </div>
  );
}

export default App;
```

Link to code example: https://codesandbox.io/p/sandbox/sleepy-resonance-29sgks

## The current behavior
It fails with "Failed to execute 'removeChild on 'Node': [..]"
This error message typically indicates that somebody or something has manipulated the DOM outside of React. However, as you can see in the very small reproducible example, this should not be the case.

I am able to reliably reproduce this on Google Chrome, but **not** Safari or Firefox. I tested on two different computers (both running OSX).
I could reproduce with a project set up with three separate environments; using vite, create-react-app, and inside codesandbox.
I also tried downgrading to react 17.0.2, and same problem there.

If the size of the list is reduced, the crash either stops or does not happen as often.

## The expected behavior
I should be able to re-render components based on state.
