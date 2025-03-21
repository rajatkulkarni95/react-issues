# Bug: [PPR] Resume failed when "moduleLoading === undefined" in function prepareDestinationWithChunks 

> Issue #28658 - Created on 3/27/2024

> Original URL: https://github.com/facebook/react/issues/28658

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
experimental
## Steps To Reproduce
```tsx
const serverResponse = createFromReadableStream(renderStream, {
  ssrManifest: {
    moduleMap: ssrModuleMapping,
    // This way can also solve the error
    // moduleLoading: null,
  },
});
// Both prerender and resume faild when ssrManifest.moduleLoading === undefined
// <Root /> comes from serverResponse 
const { prelude, postponed } = await prerenderToNodeStream(
  <Root />,
  prerenderOptions
);
const { pipe } = await resumeToPipeableStream(
  <Root />,
  postponed,
  resumeOptions
);
```

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

## The current behavior
TypeError: Cannot read properties of undefined (reading 'prefix') at prepareDestinationWithChunks 
```typescript
export function prepareDestinationWithChunks(
  moduleLoading: ModuleLoading,
  // Chunks are double-indexed [..., idx, filenamex, idy, filenamey, ...]
  chunks: Array<string>,
  nonce: ?string,
) {
  if (moduleLoading !== null) {
    for (let i = 1; i < chunks.length; i += 2) {
      preinitScriptForSSR(
        moduleLoading.prefix + chunks[i],
        nonce,
        moduleLoading.crossOrigin,
      );
    }
  }
}
```
## The expected behavior
```typescript
// In fact, this is not a bug in the general sense, but it may make prepareDestinationWithChunks more rigorous.
export function prepareDestinationWithChunks(
  moduleLoading: ModuleLoading,
  // Chunks are double-indexed [..., idx, filenamex, idy, filenamey, ...]
  chunks: Array<string>,
  nonce: ?string
) {
  // or if (moduleLoading) {}
  if (moduleLoading !== null && moduleLoading !== undefined) {
    for (let i = 1; i < chunks.length; i += 2) {
      preinitScriptForSSR(
        moduleLoading.prefix + chunks[i],
        nonce,
        moduleLoading.crossOrigin
      );
    }
  }
}
```


