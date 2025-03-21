# Bug: Inconsistent back-navigation behaviour in incognito/private browser windows

> Issue #29012 - Created on 5/7/2024

> Original URL: https://github.com/facebook/react/issues/29012

## Description

### Description
My react web application navigates to an external site on clicking a button. On the external site, if I click the back button in the browser, I get redirected back to my react application. Now: 
* in an incognito window, the react application maintains the state that was set before redirecting.
* in a non-incognito window, the react application "resets" its state to the default state.

Note: I am unable to recreate this inconsistency locally (i.e. via running the react app with `npm run start`). I have only observed this in a production-ized build in an incognito window.

### Minimum Reproducible Example
I have prepared a minimal example that does the following:
1. Click button on page to get redirected
2. Clicking the button toggles a state variable to `true`, which re-renders the page to hide the button and show "redirecting" text instead
3. After waiting 3 seconds, redirect to external page (example.com) via `window.location.href`
4. On external site, click the browser back button
5. Return to react app

**Behaviour in non-incognito window:**
Here, the page gets reset and the state variable has its default value of `false`
[Screencast from 2024-05-07 15-19-54.webm](https://github.com/facebook/react/assets/47204059/29e4b4ea-4768-43fc-b1fc-0cd3da88ecf9)

**Behaviour in incognito window:**
Here, the page maintains the state before navigation, and the state variable maintains value `true`
[Screencast from 2024-05-07 15-22-10.webm](https://github.com/facebook/react/assets/47204059/1c4755f0-badb-4369-98e2-6c8ef2109e34)

Application code:
```
import { useState } from 'react';

function App() {
  const [redirecting, setRedirecting] = useState(false);

  return (
    <div className='App'>
      {redirecting && <p>redirecting...</p>}
      {!redirecting && (
        <button
          onClick={async () => {
            setRedirecting(true);
            setTimeout(
              () => (window.location.href = 'https://example.com'),
              3000
            );
          }}
        >
          Click to redirect
        </button>
      )}
    </div>
  );
}

export default App;

```

**Browsers I have tried recreating this on:**
1. Chrome (inconsistency exists between incognito window and non-incognito window)
2. Firefox (inconsistency exists between private window and non-private window)
3. Safari (inconsistency exists between private window and non-private window)


**React version**: 17.0.2

## Steps To Reproduce

As mentioned earlier, I have only been able to recreate the inconsistency in a production-ized build of my react application. I have deployed my minimal reproducible example via Netlify, the URL is: https://master--animated-lily-d6cfcf.netlify.app/

Alternately, you may deploy a version of the application yourself (see links to code example)

1. Open productionized react app in incognito window
2. Click button "click to redirect", this sets the state variable value from `V1` to `V2`
3. Navigate to external website
4. Click back button in browser on external website
5. On return to react app, the state variable will maintain value `V2`

**Link to code example:**

Production-ized build: https://master--animated-lily-d6cfcf.netlify.app/

Source code: https://github.com/pranay1208/ext_nav_min

## The current behavior
In incognito mode, app maintains the state it had before navigation

In non-incognito mode, app resets to default state

## The expected behavior
Consistent behaviour in incognito and non-incognito windows; i.e. either state resets on back navigation, or state is maintained on back navigation
