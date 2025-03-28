# Bug: `recommended-latest` config not available in `eslint-plugin-react-hooks`

> Issue #32431 - Created on 2/20/2025

> Original URL: https://github.com/facebook/react/issues/32431

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->
According to the docs for `eslint-plugin-react-hooks`, there should be a flat config compatible config available at `reactHooks.configs['recommended-latest']`. The only config that exists in the version published on npm is `recommended`, which does not work with ESLint 9 and flat config.

By exploring the code on npm, we can see that the configs are missing
https://www.npmjs.com/package/eslint-plugin-react-hooks/v/5.1.0?activeTab=code

React version: 19.0.0

## Steps To Reproduce

1. Install ESLint 9
2. Install `eslint-plugin-react-hooks`
3. Add `reactHooks.configs['recommended-latest']` in your eslint config
4. Try to run linting

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://stackblitz.com/edit/vitejs-vite-cbgqvmqn?file=eslint.config.js&view=editor

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

When running linting after setting up as expected, an error is thrown since undefined is not a valid ESLint config object. The `recommended-latest` and `recommended-legacy` shared configs described in the readme are missing from the published package.

## The expected behavior

The plugin should include the configs the readme claims it includes. It is possible to work around the issue by manually including the contents of the config, but this defeats the point of including a shared config at all. This workaround actually seems to be what StackBlitz is doing in their React template (you can see it commented out in the provided example's `eslint.config.js`).

