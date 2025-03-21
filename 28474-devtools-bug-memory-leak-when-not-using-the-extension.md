# [DevTools Bug]: Memory leak when not using the extension

> Issue #28474 - Created on 3/1/2024

> Original URL: https://github.com/facebook/react/issues/28474

## Description

### Website or app

https://example.com

### Repro steps

1. use Firefox normally, not opening the browser dev tools at all
2. notice that the browser is getting sluggish due to continual GC, and that Firefox indicates that browser extensions are using 2GiB+
3. disable react dev tools, and observe immediate improvement in memory usage and GC CPU usage

`about:memory` diff, before and after disabling react dev tools:

```
extension (pid NNN)
Explicit Allocations

-1,894.73 MB (100.0%) -- explicit
├──-1,684.24 MB (88.89%) -- js-non-window
│  ├──-1,669.75 MB (88.13%) -- zones/zone(0xNNN)
│  │  ├──-1,610.78 MB (85.01%) -- realm([System Principal], shared JSM global)
│  │  │  ├──-1,610.79 MB (85.01%) -- classes
│  │  │  │  ├────-451.06 MB (23.81%) -- class(Map)/objects
│  │  │  │  │    ├──-360.85 MB (19.04%) -- malloc-heap
│  │  │  │  │    │  ├──-360.85 MB (19.04%) ── misc
│  │  │  │  │    │  └────-0.00 MB (00.00%) ── slots
│  │  │  │  │    └───-90.21 MB (04.76%) ── gc-heap
│  │  │  │  ├────-360.87 MB (19.05%) -- class(Function)/objects
│  │  │  │  │    ├──-360.87 MB (19.05%) ── gc-heap
│  │  │  │  │    └────-0.00 MB (00.00%) ── malloc-heap/slots
│  │  │  │  ├────-219.10 MB (11.56%) -- class(Object)/objects
│  │  │  │  │    ├──-167.54 MB (08.84%) ── gc-heap
│  │  │  │  │    └───-51.56 MB (02.72%) -- malloc-heap
│  │  │  │  │        ├──-51.56 MB (02.72%) ── slots
│  │  │  │  │        └───-0.00 MB (00.00%) ── elements/normal
│  │  │  │  ├────-212.20 MB (11.20%) -- class(Set)/objects
│  │  │  │  │    ├──-167.09 MB (08.82%) -- malloc-heap
│  │  │  │  │    │  ├──-167.09 MB (08.82%) ── misc
│  │  │  │  │    │  └─────0.00 MB (-00.00%) ── slots
│  │  │  │  │    └───-45.10 MB (02.38%) ── gc-heap
│  │  │  │  ├────-161.10 MB (08.50%) ── class(Call)/objects/gc-heap
│  │  │  │  ├────-115.99 MB (06.12%) -- class(LexicalEnvironment)/objects
│  │  │  │  │    ├──-115.99 MB (06.12%) ── gc-heap
│  │  │  │  │    └────-0.00 MB (00.00%) ── malloc-heap/slots
│  │  │  │  ├─────-45.34 MB (02.39%) -- class(Array)/objects
│  │  │  │  │     ├──-45.34 MB (02.39%) ── gc-heap
│  │  │  │  │     └───-0.00 MB (00.00%) ── malloc-heap/slots
│  │  │  │  ├─────-45.11 MB (02.38%) ── class(Proxy)/objects/gc-heap
│  │  │  │  └──────-0.01 MB (00.00%) ++ (6 tiny)
│  │  │  └───────0.01 MB (-00.00%) ++ (5 tiny)
│  │  ├─────-40.03 MB (02.11%) -- compartments
│  │  │     ├──-40.03 MB (02.11%) ── cross-compartment-wrapper-tables
│  │  │     └───-0.00 MB (00.00%) ── private-data
│  │  └─────-18.94 MB (01.00%) ++ (19 tiny)
│  └─────-14.49 MB (00.76%) ++ (3 tiny)
├────-137.46 MB (07.25%) -- window-objects
│    ├──-138.79 MB (07.33%) -- top(moz-extension://98c06d52-ba9c-4097-8d95-cfd0565b93d5/_generated_background_page.html, id=NNN)
│    │  ├──-135.99 MB (07.18%) -- active/window(moz-extension://98c06d52-ba9c-4097-8d95-cfd0565b93d5/_generated_background_page.html)
│    │  │  ├──-135.73 MB (07.16%) -- js-realm(moz-extension://98c06d52-ba9c-4097-8d95-cfd0565b93d5/_generated_background_page.html)
│    │  │  │  ├──-135.72 MB (07.16%) -- classes
│    │  │  │  │  ├───-90.48 MB (04.78%) -- class(Function)/objects
│    │  │  │  │  │   ├──-90.48 MB (04.78%) ── gc-heap [-]
│    │  │  │  │  │   └───-0.01 MB (00.00%) ── malloc-heap/slots
│    │  │  │  │  ├───-45.10 MB (02.38%) -- class(Call)/objects
│    │  │  │  │  │   ├──-45.10 MB (02.38%) ── gc-heap [-]
│    │  │  │  │  │   └───-0.00 MB (00.00%) ── malloc-heap/slots
│    │  │  │  │  └────-0.13 MB (00.01%) ++ (4 tiny)
│    │  │  │  └────-0.01 MB (00.00%) ++ sundries
│    │  │  └────-0.26 MB (00.01%) ++ (3 tiny)
│    │  └────-2.80 MB (00.15%) ++ js-zone(0xNNN)
│    └─────1.33 MB (-00.07%) ++ (8 tiny)
├─────-73.74 MB (03.89%) -- heap-overhead
│     ├──-59.05 MB (03.12%) -- bin-unused
│     │  ├──-26.77 MB (01.41%) ── bin-128
│     │  ├──-19.63 MB (01.04%) ── bin-80
│     │  └──-12.65 MB (00.67%) ++ (44 tiny)
│     └──-14.70 MB (00.78%) ++ (2 tiny)
└───────0.71 MB (-00.04%) ++ (7 tiny)
```

unfortunately, due to https://bugzilla.mozilla.org/show_bug.cgi?id=1766271, I'm unable to get any more detail on what exactly is consuming all this memory.

### How often does this bug happen?

Every time

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
