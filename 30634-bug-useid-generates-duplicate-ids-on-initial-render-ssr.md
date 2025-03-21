# Bug: useId generates duplicate IDs on initial render (ssr)

> Issue #30634 - Created on 8/8/2024

> Original URL: https://github.com/facebook/react/issues/30634

## Description

I am experiencing an issue with the useId hook in React where it generates duplicate IDs on the initial render, the problem disappear when JS hydrate the page.

React version: ^18.3.0
Remix version: ^2.9.1

## Steps To Reproduce

1. To see the error : https://validator.w3.org/nu/?showsource=yes&showoutline=yes&showimagereport=yes&doc=https%3A%2F%2Fwww.copinesdevoyage.com%2F#l1c2874
2. Or go to https://www.copinesdevoyage.com/ and disable JS
3. The duplicated ids will be found on avatars

## The current behavior
On the initial render, useId hook generates duplicate IDs


## The expected behavior
useId should produce a unique ID, ensuring that no two components have the same ID.
