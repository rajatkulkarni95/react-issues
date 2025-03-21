# [React 19] renderToReadableStream + bun.sh

> Issue #30553 - Created on 8/1/2024

> Original URL: https://github.com/facebook/react/issues/30553

## Description

## Summary

> Linux 5.15.0-116-generic x86_64 x86_64


### to reproduce it.

> install bun.sh

package.json
```json
{
  "name": "test",
  "module": "index.tsx",
  "type": "module",
  "devDependencies": {
    "@types/bun": "latest",
    "@types/react-dom": "^18.3.0",
    "@types/react": "18.3.3"
  },
  "peerDependencies": {
    "typescript": "^5.5.4"
  },
  "dependencies": {
    "react-router-dom": "^6.25.1",
    "react-dom": "next",
    "react": "next"
  }
}
```

install all
```bash
bun i
```

*index.tsx*:
```tsx
import { renderToReadableStream } from "react-dom/server";

Bun.serve({
    port: 3090,
    fetch: async (request, server) => {

        const stream = await renderToReadableStream(
            <h1>Render Test</h1>
        );

        return new Response(stream, { status: 200 });
    }
})
```

*.env file*:
```env
NODE_ENV=production
```

```bash
bun index.tsx
```

## temporal fix.

I was able to identify that in `react-dom\cjs\react-dom-server.bun.production.js` there is a type called REACT_ELEMENT_TYPE, which does not match the current node.$$type.

Their values are different:

> REACT_ELEMENT_TYPE = Symbol.for("react.transitional.element")

> node.$$type = Symbol("react.element")

temporal fix adding and modify:
```js
var React = require("react"),
ReactDom = require("react-dom),
  REACT_ELEMENT_TYPE = Symbol.for("react.element"),
  REACT_TRANSITIONAL_ELEMENT_TYPE = Symbol.for("react.transitional.element"),
  ...
  ```
  
  and:
  

```js
function retryNode(request, task){
...
  if(null !== node){
    if ("object" === typeof node) {
      switch(node,$typeof){
        case REACT_ELEMENT_TYPE:
        case REACT_TRANSITIONAL_ELEMENT_TYPE: // same as REACT_ELEMENT_TYPE

        default:
          //throw errors here also, for easy read in the console.
      }
    }
  }
...
}
```
