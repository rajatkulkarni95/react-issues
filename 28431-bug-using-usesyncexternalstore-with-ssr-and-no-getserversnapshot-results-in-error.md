# Bug: Using useSyncExternalStore with SSR and no getServerSnapshot results in error

> Issue #28431 - Created on 2/23/2024

> Original URL: https://github.com/facebook/react/issues/28431

## Description

React version: 18.2.0

## Steps To Reproduce

1. Use useSyncExternalStore and omit the third argument
2. Server render this and observe the error

Link to code example: https://stackblitz.com/edit/stackblitz-starters-n87byy

```js
import {useSyncExternalStore, Suspense, createElement} from 'react'
import * as ReactDOMServer from 'react-dom/server'

const mediaQuery = '(max-width: 600px)'
function getSnapshot() {
  return window.matchMedia(mediaQuery).matches
}

function subscribe(callback) {
  const mediaQueryList = window.matchMedia(mediaQuery)
  mediaQueryList.addEventListener('change', callback)
  return () => {
    mediaQueryList.removeEventListener('change', callback)
  }
}

function NarrowScreenNotifier() {
  const isNarrow = useSyncExternalStore(subscribe, getSnapshot)
  return createElement(
    'div',
    {},
    isNarrow ? 'You are on a narrow screen' : 'You are on a wide screen',
  )
}

function App() {
  return createElement('div', {
    children: [
      "Here's the notifier:",
      createElement(Suspense, {
        fallback: '',
        children: createElement(NarrowScreenNotifier),
      }),
    ],
  })
}

console.log(ReactDOMServer.renderToString(createElement(App)))
```

## The current behavior

The output of running this program shows:

```
<div>Here&#x27;s the notifier:<!--$!--><template data-msg="Missing getServerSnapshot, which is required for server-rendered content. Will revert to client rendering." data-stck="
    at NarrowScreenNotifier
    at Suspense
    at div
    at App"></template><!--/$--></div>
```

## The expected behavior

As noted in [the useSyncExternalStore server rendering docs](https://react.dev/reference/react/useSyncExternalStore#adding-support-for-server-rendering):

> If there is no meaningful initial value for the server rendering, omit this argument to [force rendering on the client.](https://react.dev/reference/react/Suspense#providing-a-fallback-for-server-errors-and-client-only-content)

So omitting the third argument is what you're supposed to do to force client-only rendering for cases like this (where it's impossible to know on the server what the value should be).

However, when I attempt to omit the third argument I get hydration errors. In a more complete example with Remix, I get 500 errors on the server when I do this: https://stackblitz.com/edit/remix-run-remix-su1mep

## Suggestion

Either:
1. Do not error out when omitting the third argument and instead render the suspense fallback until the client can take over
2. Update the docs to not recommend omitting the third argument

