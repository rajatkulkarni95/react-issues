# Bug: eslint-plugin-react-hooks still links to legacy.reactjs.org

> Issue #28314 - Created on 2/13/2024

> Original URL: https://github.com/facebook/react/issues/28314

## Description

~React~ `eslint-plugin-react-hooks` version: 4.6.0

## Steps To Reproduce

1. Visit https://www.npmjs.com/package/eslint-plugin-react-hooks
2. Click the [Rules of Hooks](https://legacy.reactjs.org/docs/hooks-rules.html#eslint-plugin) link

Link to code example: n/a

## The current behavior

The link points to https://legacy.reactjs.org/docs/hooks-rules.html#eslint-plugin

## The expected behavior

That page has a big _"This site is no longer updated. [Go to react.dev](https://react.dev/blog/2023/03/16/introducing-react-dev)"_ disclaimer on top. Doesn't exactly strike confidence in the lint plugin.

Could it link to https://react.dev/learn/editor-setup#linting instead?
