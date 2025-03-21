# Bug: Receiving `Error: Should have a queue. This is likely a bug in React. Please file an issue` on usage of `next-safe-action`'s `useAction` hook

> Issue #29926 - Created on 6/18/2024

> Original URL: https://github.com/facebook/react/issues/29926

## Description

React version:
`18.3.1`

## Steps To Reproduce

1. Navigate to `/apps/web`
2. Run `npm run dev` to start the local Next.js Dev server
3. Navigate to `/` route (Home)

Link to code example:
[Link to the problematic code line in one of the repository files](https://github.com/vnikolaew/TurboText/blob/main/apps/web/components/editor/hooks/useSaveLatestUserRun.tsx#L37)

Link to GitHub Project Repository:
[TurboText](https://github.com/vnikolaew/TurboText)

## The current behavior
React / Next,js errors out with the following exception:

![image](https://github.com/facebook/react/assets/88240961/e31fdd8c-907d-46af-931f-595a2ad88b59)


## The expected behavior
React to not throw any unexpected errors.

