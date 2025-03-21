# Bug: Event handling with portals is broken

> Issue #28863 - Created on 4/18/2024

> Original URL: https://github.com/facebook/react/issues/28863

## Description

Event handling with portals is broken in the newest version when placing non-react event handlers BETWEEN other react event handlers. With the following setup **outer react event handler with stopPropagation** > **non-react event handler** > **inner react event handler (in portal)**. Doing the same without portals works correctly. 

React version: 18.2.0

## Steps To Reproduce
### With portal (not working)
1. https://stackblitz.com/edit/ag-grid-react-hello-world-kag1v7?devtoolsheight=33&file=index.js
2. Click on the div
3. Only inner and outer event handlers are called

### Without portal (working)
1. https://stackblitz.com/edit/ag-grid-react-hello-world-gi5bmo?devtoolsheight=33&file=index.js
2. Comment out the portal code and comment in the non-portal code (line 24 / 25)
3. Click on the div
4. All three event handlers are triggered

Link to code example: https://stackblitz.com/edit/ag-grid-react-hello-world-gi5bmo?devtoolsheight=33&file=index.js

## The current behavior

Non-react event handlers are not called when the initial event is initiated from a portal component and an outer react event handler calls stop propagation. This works correctly without portals.

## The expected behavior

The non-react event handler should also be called when a portal component initiates the event.

## Original issue

https://github.com/facebook/react/issues/20901 was closed due to inactivity but is still valid in the newest version, see updated code examples.
