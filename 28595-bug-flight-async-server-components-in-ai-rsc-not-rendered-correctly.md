# Bug: [Flight] Async server components in `ai/rsc` not rendered correctly

> Issue #28595 - Created on 3/20/2024

> Original URL: https://github.com/facebook/react/issues/28595

## Description

When returning an async server component from an `ai/rsc` tool's `render` function, a reference to it is not serialized as a lazy node, even though it might not have been emitted as a row yet. Currently the React Flight Client is not resilient to this. This leads to the reference not being resolved correctly, and then `null` is rendered instead of the element.

The bug was introduced with #28283.

React version: 18.3.0-canary-6c3b8dbfe-20240226 (via Next.js v14.2.0-canary.30)

## Steps To Reproduce

1. Build `ai/rsc` example according to https://sdk.vercel.ai/docs/concepts/ai-rsc#build-your-app
2. Move data fetching from `render` function to an async server component

(It's probably also reproducible by writing a unit test that replicates what's being done in https://github.com/vercel/ai/blob/main/packages/core/rsc/utils.tsx#L17-L50. I might try this later... [done](https://github.com/facebook/react/pull/28601))

Link to code example: https://github.com/unstubbable/ai-rsc-test/pull/1
This contains the code of step 2 from above, has more details about the expected and actual RSC responses, and also shows in the comments how I arrived at my conclusion.
