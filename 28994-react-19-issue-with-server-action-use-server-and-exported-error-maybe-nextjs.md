# [React 19] Issue with server action "use server" and exported error (Maybe NextJS)

> Issue #28994 - Created on 5/5/2024

> Original URL: https://github.com/facebook/react/issues/28994

## Description

Hi,

Not sure if this is related to NextJS or React.

exporting an enum from a server action in a file with `"use server"` results in 

```
Error: A "use server" file can only export async functions, found object.
```

Ok, perfect.

Now just add a `use client` to your page. No more error.

In my example I try to print `Object.values(ContactFormTopics)` which gives me an empty array. This is error-prone, maybe we need a way to detect such use case

https://codesandbox.io/p/devbox/old-voice-mt3592?file=%2Fapp%2Fpage.tsx
