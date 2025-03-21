# Bug: putting promise into JSX will cause hydration issue

> Issue #27778 - Created on 12/3/2023

> Original URL: https://github.com/facebook/react/issues/27778

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.0-canary-5dd35968b-20231201

## Steps To Reproduce

1. clone https://github.com/himself65/react-hydration-error
2. pnpm install && pnpm run dev

Link to code example:

```js
import { Component } from '@/components/component'

export default function Home () {
  const delayedMessage = new Promise((resolve) => {
    setTimeout(() => resolve('Hello from server!'), 2000)
  })
  return (
    <main>
      <div>
        <Component delayedMessage={delayedMessage}/>
      </div>
    </main>
  )
}
```

```js
"use client"
export function Component ({
  delayedMessage
}) {
  return (
    <div>
      {delayedMessage}
    </div>
  )
}
```

## The current behavior

![image](https://github.com/facebook/react/assets/14026360/1d6a91d3-b36b-40d6-aad4-f709525e66bb)

## The expected behavior

Won't have hydration error

