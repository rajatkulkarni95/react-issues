# Bug: <link> onLoad event happened but not triggered (18.2.0 & 18.3.0-canary-2e470a788-20240214)

> Issue #28356 - Created on 2/16/2024

> Original URL: https://github.com/facebook/react/issues/28356

## Description

I don't seem to be able to trigger onLoad on the link element. Browser reports that the element was loaded and not used.

React version: 18.2.0 (stable) & 18.3.0-canary-2e470a788-20240214

## Steps To Reproduce

1. render html page on the server with `renderToPipeableStream`, get this content: `<!DOCTYPE html><html lang="en"><head><link id="initial-style" rel="preload" href="/assets/main.56751cdb86e2b7c07557.css" as="style"/>...`
2. `hydrateRoot` on the client
3. browser reports that the link element has loaded and has not been used, the onLoad function is not triggered

Component code used:

```jsx
const [ stylesheetLoaded, setStylesheetLoaded ] = useState(false)

  return (
    <html lang="en">
      <head>
        {
          initialStylePath &&
            <>
              <link id="initial-style"
                rel={stylesheetLoaded ? 'stylesheet' : 'preload'}
                as="style"
                href={initialStylePath}
                onLoad={() => {setStylesheetLoaded(true); console.log('stylesheet loaded')}} />
              <noscript><link rel="stylesheet" href={initialStylePath} /></noscript>
            </>
        }
```

I am applying this pattern: https://web.dev/articles/defer-non-critical-css

## The current behavior

- Chrome console reports `The resource http://localhost:8080/assets/main.56751cdb86e2b7c07557.css was preloaded using link preload but not used within a few seconds from the window's load event. Please make sure it has an appropriate `as` value and it is preloaded intentionally.`
- The even does not trigger
- inspector still shows the link element as `rel="preload"`

## The expected behavior

- The event should trigger.
- Chrome console should not display the warning.
- `rel` should update to `stylesheet`.
