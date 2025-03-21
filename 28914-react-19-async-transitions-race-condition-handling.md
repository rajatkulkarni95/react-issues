# [React 19] Async transitions race condition handling

> Issue #28914 - Created on 4/26/2024

> Original URL: https://github.com/facebook/react/issues/28914

## Description

## Summary

Repro: https://stackblitz.com/edit/vitejs-vite-ymbqrc?file=src%2FApp.tsx

How do we handle async transitions that resolve out of order? In the above reproduction the search for "a" can resolve after "ab", leading to the input containing "ab" but the results pertaining to "a". In other words, the most recent transition isn't the one that wins.

In other discussions it's [been mentioned](https://twitter.com/acdlite/status/1768780638767788501) that this is caused by React losing the context that the setState happens inside a transition as it happens after `await`. But I'm not sure how to work around this today
