# Bug: Uncaught DOMException: Failed to set the 'value' property on 'HTMLInputElement': This input element accepts a filename, which may only be programmatically set to the empty string.

> Issue #28570 - Created on 3/16/2024

> Original URL: https://github.com/facebook/react/issues/28570

## Description

uploading a file that I read with readAsDataUrl creates this error

React version:
 "react": "18.2.0",
 "react-dom": "18.2.0",

## Steps To Reproduce

1. Create an input type=file
2. Upload a file and read it with readAsDataUrl
3. Store the result in a state
4. Use this state to display the result

Link to code example: https://stackblitz.com/edit/stackblitz-starters-u1i4q1?file=app%2FhomeChild.tsx

## The current behavior

creates an error

## The expected behavior

not creating an error, being able to upload a file
