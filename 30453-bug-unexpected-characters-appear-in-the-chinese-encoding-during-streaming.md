# Bug: Unexpected characters appear in the Chinese encoding during streaming

> Issue #30453 - Created on 7/25/2024

> Original URL: https://github.com/facebook/react/issues/30453

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
18.3.1

## Steps To Reproduce

When I use remix to stream render a page, sometimes garbled characters appear on the page when my data contains Chinese characters. I saw through debugging that react-dom inserts null characters when parsing, which causes an exception during merging.

https://github.com/facebook/react/blob/76002254b7e3270da199eec1e6f9a0577b988a36/packages/react-server/src/ReactServerStreamConfigNode.js#L75

![img_v3_02d4_942e9e0c-fa2a-4465-af45-b9aa00e80d6g](https://github.com/user-attachments/assets/be367317-8b69-4abe-9eb5-ada93cb567ec)
![img_v3_02d4_7b3ede95-8807-4f12-9214-d160ed0f7e9g](https://github.com/user-attachments/assets/81215192-8c54-4eb0-b9fc-df010346e2f0)

and when `textEncoder.encodeInto` exec
![img_v3_02d4_e966adc3-c565-4b4c-abdc-0fa90a5eb0eg](https://github.com/user-attachments/assets/d8ce12c6-0ffc-4e62-a2b0-cc7bee388a2d)

Due to business issues, I can only provide a short reproducible fragment

```js
var util = require('util')

var textEncoder = new util.TextEncoder()

var target = new Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

textEncoder.encodeInto(
  '__remixContext.r("routes/page.$pageName", "getConfig", {"headTitle":"升级有礼","title":"有礼升级至新版立得块优惠券20"',
  target
)
console.log(new TextDecoder().decode(target))
// result: __remixContext.r("routes/page.$pageName", "getConfig", {"headTitle":"升级有礼","title":"有��
```

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

## The current behavior

When transmitting Chinese data, sometimes garbled code can occur

## The expected behavior

streaming original data
