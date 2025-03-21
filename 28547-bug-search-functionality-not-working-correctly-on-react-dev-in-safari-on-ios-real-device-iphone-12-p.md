# Bug: Search functionality not working correctly on react.dev in Safari on iOS real device (iPhone 12 Pro)

> Issue #28547 - Created on 3/13/2024

> Original URL: https://github.com/facebook/react/issues/28547

## Description

## Steps To Reproduce

1. Open react.dev in Safari on iPhone (real device)
2. Tap search icon: note that search function is working as intended
3. Scroll down to "Write components with code and markup" section
4. Tap search icon: note that action doesn't open search
5. Scroll down again and tap the search icon several times:  note that action doesn't open search
6. Repeat step 5: note that eventually screen freezes

An issue has been opened in the [react.dev repo as well](https://github.com/reactjs/react.dev/issues/6694)
---

## The current behavior
Search functionality does not work correctly on iOS real device (iPhone 12 Pro). 

https://github.com/facebook/react/assets/57572988/72673d2b-0d83-4bcd-b851-565eff6155b7

Since search functionality is currently working as expected on macOS, both in Chrome and Safari, the issue might be in implementation of [Algolia InstantSearch iOS](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/ios/):

https://github.com/facebook/react/assets/57572988/9878e087-2ec3-4227-85aa-6e3cc79d7a8d

The iOS real device that this behavior was recorded on is using the current iOS version:

![react_github-bug-report_ios-version](https://github.com/facebook/react/assets/57572988/2bd0c2d5-bb46-43ae-b934-e16e9e6a33e6)

---

## The expected behavior

Search functionality is working as expected on macOS, both in Chrome and Safari. Should work similarly on iOS real device:

**macOs Chrome**

https://github.com/facebook/react/assets/57572988/07dd29d9-fb96-45a7-bdbc-d1d320ed8117

**macOS Safari**

https://github.com/facebook/react/assets/57572988/ac1e01e0-f8e9-4270-bb6e-bed47b9f8a17
