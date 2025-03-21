# [ReadToPipeableStream] Support { end: false } Options as second param

> Issue #28082 - Created on 1/25/2024

> Original URL: https://github.com/facebook/react/issues/28082

## Description

React's ReadToPipeableStream currently behaves inconsistently with other Node.js streams in terms of the pipe function it returns. It automatically calls the end method of the target stream when it finishes. This prevents users from manually controlling the target stream and inserting desired data. If one wants to insert a script, they have to resort to alternatives like what Remix does: https://github.com/remix-run/remix/blob/main/packages/remix-react/components.tsx#L943-L973. However, all other streams in Node.js can be piped with pipe(writable, {end:false}). I believe that this control should be handed over to the users.


Related react code: https://github.com/facebook/react/blob/main/packages/react-server/src/ReactServerStreamConfigNode.js#L194-L196
