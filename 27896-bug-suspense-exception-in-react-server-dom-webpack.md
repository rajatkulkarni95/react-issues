# Bug: Suspense Exception in react-server-dom-webpack

> Issue #27896 - Created on 1/8/2024

> Original URL: https://github.com/facebook/react/issues/27896

## Description

I just began using Sentry in the Next project I'm currently working on and found relatively quickly that a very weird error is being thrown in production at: (react-server)/./dist/compiled/react-server-dom-webpack/cjs/react-server-dom-webpack-server.edge.production.min.js at line 12:123419

The error in Sentry states the following: 
Suspense Exception: This is not a real error! It's an implementation detail of `use` to interrupt the current render. You must either rethrow it immediately, or move the `use` call outside of the `try/catch` block. Capturing without rethrowing will l...

Hosting this project on Vercel. 

React version: 18.2.0
Node version: 20.9.0

## The current behavior
An error is being thrown even though it states it is not a real error.

## The expected behavior
The error should not be thrown if it is not a real error. 

