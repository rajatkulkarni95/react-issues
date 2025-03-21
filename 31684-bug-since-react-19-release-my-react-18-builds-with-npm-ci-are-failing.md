# Bug: Since React 19 release my React 18 builds with npm ci are failing

> Issue #31684 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31684

## Description

As soon as React 19 was published on December 5, 2024 approx 4:05PM EST, all my builds for React 18 (18.3.1) in my CICD pipeline are failing with Linting and Types errors raised from when `yarn build` is building my Next JS v 14.0.4 app.

React version: 18.3.1

Before the release, I was able to build my React 18 app without issue, I was building dozens per day. As soon as the React 19 was published it all broke. Any reason for this? I have React 18.3.1 locked in my package.json, my dependency versions are all the same. Did something change with React 18.3.1 version?
