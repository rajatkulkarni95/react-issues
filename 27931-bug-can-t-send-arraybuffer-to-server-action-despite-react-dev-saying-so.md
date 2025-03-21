# Bug: Can't send ArrayBuffer to Server Action despite react.dev saying so

> Issue #27931 - Created on 1/12/2024

> Original URL: https://github.com/facebook/react/issues/27931

## Description

Can't send ArrayBuffer to Server Action despite [react.dev](https://react.dev/reference/react/use-server#serializable-parameters-and-return-values) saying that you can. I'm not sure if this is an error or my part or the documentation. I retrieved the arrayBuffer from file of formData, then pass it through the parameter of the Server Action.

It seems like it doesn't get sent to the server because it can't be parsed due to ArrayBuffer being serializable but not iterable. 

However this is somewhat confusing because you can attach File in FormData in the form of Blob and send it to the Server Action.

I understand that FormData is [handled separately](https://github.com/facebook/react/blob/0ac3ea471fbcb7d79bc7d36179e960c72c779e76/packages/react-client/src/ReactFlightReplyClient.js#L238) but I'm not sure I understand why it can't be done the same with ArrayBuffer.

I understand that I can just pass the FormData to send files but In my case I needed to transform the Files first before uploading and it ends up with a Blob. 

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:

## Steps To Reproduce

1. Create form, input, submit button, and also onSubmit function using Client Action
2. Retrieve the arrayData from the formData then pass it to server action

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

https://codesandbox.io/p/devbox/nextjs-arraybuffer-server-action-36gvxn

## The current behavior

Throws client-side error


## The expected behavior

ArrayBuffer gets sent to the server

The documentation:

<img width="583" alt="image" src="https://github.com/facebook/react/assets/20208219/6c082998-f1f1-4657-8131-f5df8620bc9b">

Please let me know if I fail to understand the documentation or if it's something wrong in the documentation


