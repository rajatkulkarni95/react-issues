# [DevTools Bug]: Big Memory Leak

> Issue #28230 - Created on 2/4/2024

> Original URL: https://github.com/facebook/react/issues/28230

## Description

### Website or app

https://draco-lang.org/

### Repro steps

My firefox seriously slowed down, I tried to track down why, it turned out an extension was taking near **70GB**.  
I made a memory dump to see the issue:  

```
Explicit Allocations

75,498.45 MB (100.0%) -- explicit
├──38,653.19 MB (51.20%) ++ js-non-window
├──36,174.13 MB (47.91%) -- window-objects
│  ├──36,021.81 MB (47.71%) -- top(moz-extension://0547e6cd-9505-4377-9aed-8126cfe099f6/_generated_background_page.html, id=75)
│  │  ├──34,190.45 MB (45.29%) -- js-zone(0x1cb6863ec00)
│  │  │  ├──34,010.77 MB (45.05%) -- strings
│  │  │  │  ├──34,005.90 MB (45.04%) -- string(length=26970, copies=621562, "data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS" (truncated))
│  │  │  │  │  ├──33,991.67 MB (45.02%) ── malloc-heap/two-byte
│  │  │  │  │  └──────14.23 MB (00.02%) ── gc-heap/two-byte
│  │  │  │  └───────4.87 MB (00.01%) ++ (13 tiny)
│  │  │  └─────179.68 MB (00.24%) ++ (9 tiny)
│  │  └───1,831.36 MB (02.43%) -- active/window(moz-extension://0547e6cd-9505-4377-9aed-8126cfe099f6/_generated_background_page.html)
│  │      ├──1,831.28 MB (02.43%) -- js-realm(moz-extension://0547e6cd-9505-4377-9aed-8126cfe099f6/_generated_background_page.html)
│  │      │  ├──1,831.27 MB (02.43%) -- classes
│  │      │  │  ├────934.56 MB (01.24%) ++ class(Object)/objects
│  │      │  │  └────896.70 MB (01.19%) ++ (4 tiny)
│  │      │  └──────0.01 MB (00.00%) ++ sundries
│  │      └──────0.08 MB (00.00%) ++ (3 tiny)
│  └─────152.31 MB (00.20%) ++ (22 tiny)
└─────671.13 MB (00.89%) ++ (24 tiny)
```
I knew it was react dev tools with it's extension id: 547e6cd-9505-4377-9aed-8126cfe099f6.  
When I decoded the SVG of the string (that I truncated), I immediately recognized my own dark mode switch trick.  
I know the image is used on https://draco-lang.org/ and https://playground.draco-lang.org/, I had both tab open, and it doesn't reproduce at will. It's probably the first link since it use React.


### How often does this bug happen?

Sometimes

### DevTools package (automated)

_No response_

### DevTools version (automated)

_No response_

### Error message (automated)

_No response_

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
