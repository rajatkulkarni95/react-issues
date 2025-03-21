# Portal can't be placed inside img tag

> Issue #31681 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31681

## Description

React version: 18.2

## Steps To Reproduce

1. `<img>{ReactDOM.createPortal(<div />, document.body)}</img>`

## The current behavior

    react-dom.development.js:2942 Uncaught Error: img is a void element tag and must neither have `children` nor use `dangerouslySetInnerHTML`.

## The expected behavior

Since portal does not create actual DOM inside the image tag, it does not violate DOM rules, and it would be useful to allow it for event bubbling purposes.
