# Why react-dom/server will automatic reorder elements in head

> Issue #27879 - Created on 1/5/2024

> Original URL: https://github.com/facebook/react/issues/27879

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.0-canary-0cdfef19b-20231211

## Steps To Reproduce

I try to reorder elements in `<head>`, but I found `react` always force push some element at the top. e.g. reverse elements in head, the `<link rel="dns-prefetch">` always at the top. Just like the demo code.

The reason why I want to reorder elements is <https://github.com/rviscomi/capo.js/blob/main/src/lib/rules.js> found 

> How you order elements in the <head> can have an effect on the (perceived) performance of the page.
> This script helps you identify which elements are out of order.

So I want to reorder elements according to this repo

```
export const ElementWeights = {
  META: 10,
  TITLE: 9,
  PRECONNECT: 8,
  ASYNC_SCRIPT: 7,
  IMPORT_STYLES: 6,
  SYNC_SCRIPT: 5,
  SYNC_STYLES: 4,
  PRELOAD: 3,
  DEFER_SCRIPT: 2,
  PREFETCH_PRERENDER: 1,
  OTHER: 0
};
```

and open an abtest on my project, but looks like `react` don't want to me resort the elements. I found some code in react source code:

![image](https://github.com/facebook/react/assets/6839576/abab06b0-8fa2-4e5e-9d1c-064afc644398)

**There is any reason why react will reorder elements in <head> during rendering?** You can test via the follow code.

```tsx
import React, { Children, Suspense } from 'react'
import http from 'http'
import { renderToPipeableStream } from 'react-dom/server'

const Header = (props) => {
  return (
    <head>
      {Children.toArray(props.children).reverse()}
    </head>
  )
}

const App = () => {
  return (
    <html>
      <Header>
        <title>header</title>
        <link rel="dns-prefetch" href="https://fonts.googleapis.com" />
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      </Header>
      <body>
        <div id="root">
          hello
        </div>
      </body>
    </html>
  )
}

const app = http.createServer(async (req, res) => {
  console.log(req.url)
  const { pipe } = renderToPipeableStream(<App />, {
    onShellReady() {
      pipe(res)
    },
  })
})

app.listen(8080, () => {
  console.log('Server start at 8080')
})

app.on('error', (err) => {
  console.log(err);
})

process.on('uncaughtException', function (err) {
  console.log(err);
}); 
```

## The current behavior

![image](https://github.com/facebook/react/assets/6839576/3cf6c83d-3bc8-45f6-8a5b-5cf28ff15878)

## The expected behavior

```
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link rel="icon" type="image/svg+xml" href="/vite.svg" />
<meta charset="UTF-8" />
<link rel="dns-prefetch" href="https://fonts.googleapis.com" />
<title>header</title>
```

