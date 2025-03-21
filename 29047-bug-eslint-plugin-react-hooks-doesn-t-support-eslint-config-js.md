# Bug:  eslint-plugin-react-hooks doesn't support eslint.config.js 

> Issue #29047 - Created on 5/13/2024

> Original URL: https://github.com/facebook/react/issues/29047

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: Any

## Steps To Reproduce

1. Configure eslint-plugin-react-hooks with eslint.config.js es module config
2. It doesn't resolve react-hooks plugin

## The current behavior

Passing `...reactHooks.configs.recommended.rules`  does not resolve the plugin
![зображення](https://github.com/facebook/react/assets/167980386/af3699c3-7dcd-403b-a457-409e77dfcf97)

## The expected behavior

For the plugin to work with the modern eslint config.
