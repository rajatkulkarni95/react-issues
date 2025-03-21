# Bug: unexpected Warning: `ReactDOMTestUtils.act` is deprecated in favor of `React.act`.

> Issue #29000 - Created on 5/6/2024

> Original URL: https://github.com/facebook/react/issues/29000

## Description

I didn't use `act` in `react-dom/test-utils` but I got the following warning :
Warning: `ReactDOMTestUtils.act` is deprecated in favor of `React.act`. Import `act` from `react` instead of `react-dom/test-utils`. See https://react.dev/warnings/react-dom-test-utils for more info.

React version:18.3.1

## Steps To Reproduce

1.run `npx create-react-app test --template typescript`
2.run `cd test`
3.run `npm run test`
4.press `a`

<img width="935" alt="image" src="https://github.com/facebook/react/assets/90126412/be7dc826-3ac3-4717-9bc7-61a04091c70d">

