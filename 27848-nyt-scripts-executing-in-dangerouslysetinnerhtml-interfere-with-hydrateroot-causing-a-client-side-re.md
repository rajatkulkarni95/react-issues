# NYT: Scripts executing in `dangerouslySetInnerHTML` interfere with `hydrateRoot`, causing a client-side re-render

> Issue #27848 - Created on 12/20/2023

> Original URL: https://github.com/facebook/react/issues/27848

## Description

React version: 18.2.0

**Context:**

This is a soft follow-up to a previously reported issue with React many years ago (https://github.com/facebook/react/issues/10923).

At The New York Times, we use custom embedded interactives rendered server-side with `dangerouslySetInnerHTML`.
These interactives have their own HTML, links, and scripts, running independently of the React tree. This allows editors and journalists to inject one-off, self-contained [visual and interactive elements](https://www.nytimes.com/2023/10/27/business/kanye-west-adidas-yeezy.html?unlocked_article_code=1.HE0.UNYF.RO8H-ah7U_NG&smid=url-share) into our report without having to alter or re-deploy core infra. 

A simplified example might look something like this (where script tags will modify the DOM as soon as the page has loaded):

```js
const htmlString = `
  <div id="server-test">server</div>
  <script>
    document.addEventListener("DOMContentLoaded", () => {
      const serverTestElement = document.getElementById("server");
      serverTestElement.textContent = "client";
    });
  </script>
`;
return <div dangerouslySetInnerHTML={{ __html: htmlString }} />;
```

## The current behavior
In the current behavior the html element will appear as:

1. `<div id="server-test">server</div>` --> (initial browser load from server)
1. `<div id="server-test">client</div>` --> (script tags run, changing the text content from server to client)
1. `<div id="server-test">server</div>` --> (hydration sees a mismatch and defers to client-side render)

## The expected behavior

In the expected behavior (which existed pre React 18), the html element should appear as:
1. `<div id="server-test">server</div>` --> (initial browser mount)
1. `<div id="server-test">client</div>` --> (script tags run, changing the text content from server to client)
1. `<div id="server-test">client</div>` --> (hydration ignores dangerouslySetInnerHTML changes)

## Reasoning and Impact
This seems to be the result of the script tag manipulating the DOM element before hydration has completed, resulting in a hydration mismatch, which React has chosen to be much stricter about. This causes React to discard the server-rendered content modified by script tags and fall back to client-side rendering. 

Unfortunately, the side effect of deferring to the client side is that HTML strings that contain `<script/>` tags that are rendered via `dangerouslySetInnerHTML` will _not_ execute unless manually appended to an element such as the `<head>`. This is possible to do as a workaround by extracting each script tag manually, however, this disrupts the intended behavior where these scripts should execute immediately after browser load and creates an unintended script execution delay (and potentially other issues such as a flash of unstyled content). 

cc @acdlite and co

