# [DevTools Bug]: After updating to version 5.1 the Dev tools fails to inspect elements

> Issue #28903 - Created on 4/24/2024

> Original URL: https://github.com/facebook/react/issues/28903

## Description

### Website or app

https://riverside.fm/dashboard

### Repro steps

Upon updating to the most recent version of the development tools, I encountered a significant issue when utilizing the Components tab. Specifically, when a component incorporates a Redux-related hook, such as useDispatch, functionality within the tab fails, leading to errors such as 'Cannot read properties of undefined (reading 'dispatch').'"
![image](https://github.com/facebook/react/assets/87265670/698bb336-881b-451d-88a1-5089774cb049)
This issue appears to be directly linked to the development tools, as even upon reverting to code from two weeks ago, the problem persists. Upon inspection, it's evident that the malfunction stems from the useDispatch function, despite its status as a native React feature. This discrepancy is perplexing and suggests a potential compatibility issue between the development tools and Redux functionality.

![image](https://github.com/facebook/react/assets/87265670/27b3881d-5140-4b40-9dbd-a9b21d9187e0)


### How often does this bug happen?

Often

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
