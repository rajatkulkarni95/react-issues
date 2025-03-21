# Bug: Internal React error: Expected static flag was missing.

> Issue #28694 - Created on 3/31/2024

> Original URL: https://github.com/facebook/react/issues/28694

## Description

This error arose while implementing a feature to collapse reply comments in the comment section of a website. You can find the potentially problematic code [here](https://codesandbox.io/s/github/Fun117/my-react-issues?file=/src/components/client/elements/comments.tsx#57).

**Versions:**
- Next.js: 14.1.3
- React: 18

## Steps To Reproduce

1. Go to this [code sandbox](https://codesandbox.io/s/github/Fun117/my-react-issues).
2. Open the page.
3. Check the console for the error message.

## Additional Repositories

- Repository with the potentially problematic code: [Fun117/my-react-issues](https://github.com/Fun117/my-react-issues)
- Repository where the feature (reply comment collapsing) is planned to be added: [selcold/scratch-building](https://github.com/selcold/scratch-building)

## The current behavior

An error occurs due to the malfunctioning show/hide comments feature, particularly an unexpected internal React error.
[Error-causing file](https://codesandbox.io/s/github/Fun117/my-react-issues?file=/src/components/client/elements/comments.tsx)

## The expected behavior

The show/hide comments feature should function correctly without any errors.

