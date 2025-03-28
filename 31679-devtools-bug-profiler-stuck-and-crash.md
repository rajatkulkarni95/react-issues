# [DevTools Bug]: Profiler stuck and crash

> Issue #31679 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31679

## Description

### Website or app

Any dev or profiling build of React v16.5+, ie. https://zi8n3.csb.app/

### Repro steps

Part 1 (Stuck):
1. open profiler in react dev tools
2. click record button
3. do any action on the web page (click button or input, etc)
4. click stop record button
5. click record button again

Then you can see the profiler is stuck.

Part 2 (Crash):
6. continue from the above steps
7. close Chrome console
8. open the Chrome console again

Will see the components and profiler tabs are disappeared and you can't reopen it by clicking the extension, unless you restart the Chrome.

Note: if you clear the profiling data before step 5, everything works fine.

Env: MacOs Chrome extension
Chrome version: 131.0.6778.108


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
