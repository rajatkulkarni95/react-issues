# [DevTools Bug]: Consistent memory leak when refreshing on React + non-React websites.

> Issue #28323 - Created on 2/14/2024

> Original URL: https://github.com/facebook/react/issues/28323

## Description

### Website or app

https://google.com

### Repro steps

With Chrome version `121.0.6167.184 (Official Build) (arm64)`

React dev tools: `5.0` - `Created from revision 993c4d003 on 12/5/2023.`

Repeatedly refreshing `https://google.com` continually leaks memory. 


## With React Dev Tools

### Some memory is retained temporarily between refreshes, but notably forcing GC (the trashcan button), never shrinks + each subsequent refresh monotonically increases memory overhead. 

https://github.com/facebook/react/assets/5288805/1cc1b7b4-06c5-4ec9-aaf4-e65c8e40dffc

## Without React Dev Tools

### Forcing GC without react dev tools drops the memory footprint from ~100MB to ~10MB instantly. 

https://github.com/facebook/react/assets/5288805/29beb02b-1c16-4ec4-91f0-b732f992b72e



### Other debugging:
Went down a massive rabbithole of Chrome version bisection (memory between refreshed started to be retained a _bit_ longer with this V8 GC change), but it always GC'd correctly when being forced: https://chromium.googlesource.com/v8/v8/+/7477604415624e2f60000194f766e2f404e02fed.


### Other notes:
- This was in incognito mode without any other extensions enabled
- Happy to provide heap snapshots (it appears that retained memory is mostly `closure` + `compiled` code) + hopefully this should be simple to repro. 







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
