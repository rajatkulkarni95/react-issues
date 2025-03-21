# Bug: Fix Buffer - Write Chunks to Separate Buffers

> Issue #32176 - Created on 1/23/2025

> Original URL: https://github.com/facebook/react/issues/32176

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->
The bug happens when using ReactDOMFizzServer.renderToReadableStream to render big chunks of data. If a chunk is bigger than the buffer (default: 512 bytes), the buffer overflows or uses incomplete data. This causes wrong or cut-off output because the renderer doesn’t handle buffer size properly.

React version:
React 19.0.0

## Steps To Reproduce
1. Create a large chunk of data that is bigger than the buffer size.
2. Start processing the data using `ReactDOMFizzServer.renderToReadableStream`.  
3. Observe the behavior when the chunks exceed the buffer size.  

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->
```
import ReactDOMFizzServer from 'react-dom/server';

// Minimal data to reproduce the problem
const largeChunk = 'A'.repeat(2049); // A chunk exceeding  default 512 bytes

async function testStream() {
  //  simple React structure with the large chunk
  const stream = await ReactDOMFizzServer.renderToReadableStream(
    <div>{largeChunk}</div>
  );

  // function to read the stream
  const decoder = new TextDecoder();
  const reader = stream.getReader();
  let result = '';
  while (true) {
    const { done, value } = await reader.read();
    if (done) break;
    result += decoder.decode(value);
  }

  console.log(result);
}

testStream();
```

## The current behavior
Right now, when chunks are sent to a `ReadableStream`, they are enqueued directly without checking the buffer size. If a chunk is too big (like 2049 bytes, while the buffer is only 512 bytes), it reuses old buffers, which messes up the output. For example, instead of properly rendering, we get something like ```<div>AAAAA...</div>```.

## The expected behavior
Chunks should be written to their own buffer and split into smaller parts if they are too big. The buffer should only be sent once it's full or the writing is complete. This way, even large chunks (like 2049 bytes) will render correctly, for example: ```<div>AAAAAAAAAAAAAAAAA...</div>```.



