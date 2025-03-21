# Bug: [eslint-plugin-react-hooks] Compatibility issue with ESLint 9.x.x

> Issue #31158 - Created on 10/9/2024

> Original URL: https://github.com/facebook/react/issues/31158

## Description

It appears that `eslint-plugin-react-hooks` is not compatible with ESLint version 9.x.x. 
When attempting to use ESLint 9.x.x with `eslint-plugin-react-hooks`, I encounter dependency resolution issues, specifically that the plugin does not support ESLint 9.

Steps to reproduce:
1. Install ESLint 9.x.x along with `eslint-plugin-react-hooks`.
2. Run ESLint or install dependencies.
3. Encounter peer dependency conflict or related errors.

Expected behavior:
- `eslint-plugin-react-hooks` should support ESLint 9.x.x without errors.

Actual behavior:
- Peer dependency conflicts or errors occur during installation or usage of ESLint 9 with this plugin.

React version:     "react": "18.3.1",

Link to code example:

## The current behavior
npm install with --legacy-peer-dependencies

these are my packages
"eslint": "^9.8.0",
    "eslint-plugin-react": "7.35.0",
    "eslint-plugin-react-hooks": "4.6.0",

## The expected behavior

npm i without the legacy peer flag
