# Bug: Truffle firefox extension causes a uncaught runtime exception on fresh react app

> Issue #29152 - Created on 5/18/2024

> Original URL: https://github.com/facebook/react/issues/29152

## Description

After a few seconds of being in a fresh React app in my browser an uncaught runtime exception occurs. This is due to a failed API call that is originating from the Truffle extension. This extension should only be enabled when on select Youtube channels. My only known fix is to disable the extension.

## Error 

> Failed to call api method: could not connect to provider anyweb-to-anyweb-unprivileged-api-v1
i/</t</i</<@moz-extension://340cd744-b9a5-4f48-9d4b-e147eb049a31/transframe-provider.js:1:1551
i/</t</i<@moz-extension://340cd744-b9a5-4f48-9d4b-e147eb049a31/transframe-provider.js:1:1532
setInterval handler*i/</t<@moz-extension://340cd744-b9a5-4f48-9d4b-e147eb049a31/transframe-provider.js:1:1360
i/<@moz-extension://340cd744-b9a5-4f48-9d4b-e147eb049a31/transframe-provider.js:1:1214
@moz-extension://340cd744-b9a5-4f48-9d4b-e147eb049a31/injected-script/index.js:5:4526



React version: ^18.3.1

## Steps To Reproduce

1. Have Truffle extension enabled
2. Run any React web app

