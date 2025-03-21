# Bug: Component's redux state value resets to null even though no action to do so initiated

> Issue #28469 - Created on 2/29/2024

> Original URL: https://github.com/facebook/react/issues/28469

## Description

I have a component that seems to work fine, except when I scroll. I am trying to implement infinite scroll. And when I do a scroll and my target is found, my redux state object resets to null.

React version: 18.2.0
React Redux: 9.1.0
Redux Toolkit: 2.2.1

## Steps To Reproduce

1. Go to my repo indicated below and clone
2. Run npm install
3. Run app with npm run dev
4. Select READ button at top middle of screen
5. Enable chrome debugger to view console logs
6. Click CONNECT button on upper right side and then click Connect button on modal
7. Once you connect you should see a bunch of content items display in middle of screen (DO NOT click on the row of avatars near top of screen)
8. Notice console log has this entry "entered getData currentFollowedId: 0, profile: [object Object], priorKeyset: 0, refreshWorksList: false". Notice that profile is an object and not null
9. Scroll to bottom of item list and you should see a spinner
10. View console logs again and notice message like this "entered getData currentFollowedId: 0, profile: null, priorKeyset: 0, refreshWorksList: false". Profile should not be null since no logoff action was performed. You can view code to confirm.

Link to code example: https://github.com/jsoneaday/freeauthor

## The current behavior
My redux state value resets to default values

## The expected behavior
Excpect any values that have been set to stay as they are
