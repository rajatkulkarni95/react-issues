# Bug: Modify value of textarea value in react s page by javascript and select dropdown item  by javascript 

> Issue #28311 - Created on 2/13/2024

> Original URL: https://github.com/facebook/react/issues/28311

## Description

Hi. 
 this bug has been mentioned in previous years and posts and , but I still cannot solve my problem with the presented methods. One of the solutions that was presented and worked for other inputs was this function:

```js
function setNativeValue(element, value) {
    let lastValue = element.value;
    element.value = value;
    let event = new Event("input", { target: element, bubbles: true });
    // React 15
    event.simulated = true;
    // React 16
    let tracker = element._valueTracker;
    if (tracker) {
        tracker.setValue(lastValue);
    }
    element.dispatchEvent(event);
}
```

my browser firefox end version - os: win10 

