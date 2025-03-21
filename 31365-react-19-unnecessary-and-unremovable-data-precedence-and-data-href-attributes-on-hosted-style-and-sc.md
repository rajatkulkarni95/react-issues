# [React 19] Unnecessary and unremovable `data-precedence` and `data-href` attributes on hosted `<style>` and `<script>`.

> Issue #31365 - Created on 10/26/2024

> Original URL: https://github.com/facebook/react/issues/31365

## Description

## Summary

https://codesandbox.io/p/devbox/28rwmr

```tsx
import { Writable } from "node:stream";
import React, { StrictMode } from "react";
import { renderToPipeableStream } from "react-dom/server";

async function renderJsx(children: React.ReactNode): Promise<string> {
  return new Promise((resolve, reject) => {
    let { pipe } = renderToPipeableStream(<StrictMode>{children}</StrictMode>, {
      onAllReady: (err: unknown) => {
        if (err) {
          console.error("onAllReady", err);
          reject(err);
          return;
        }

        pipe(
          new (class extends Writable {
            #chunks: any[] = [];

            _writev(chunks: any, callback): void {
              this.#chunks.push(...chunks.map((c: any) => c.chunk));
              callback();
            }

            _final(callback: (error?: Error | null) => void): void {
              callback();
              resolve(new Blob(this.#chunks).text());
            }
          })()
        );
      },

      onShellError: reject,
    });
  });
}

renderJsx(
  <StrictMode>
    <html>
      <body>
        <style href="foo" precedence="medium">{`
          .my-p {
            color: purple;
          }
        `}</style>
      </body>
    </html>
  </StrictMode>
).then(console.log, console.error);
```

Output:

```html
<!DOCTYPE html><html><head><style data-precedence="medium" data-href="foo">
          .my-p {
            color: purple;
          }
        </style></head><body></body></html>
```

As expected this moved the style to the head but it has added unnecessary `data-precedence` and `data-href` attributes.

I don't know if these are required for rehydration but if so they should be optional for static components or static output.

Version: `19.0.0-rc-b8ae38f8-20241018`
