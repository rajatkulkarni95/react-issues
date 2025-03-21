# Bug: Uncaught ReferenceError: MessageChannel is not defined

> Issue #31827 - Created on 12/18/2024

> Original URL: https://github.com/facebook/react/issues/31827

## Description

React version: 19.0.0

## Steps To Reproduce

1. Create an Astro & React project with server adapter for Cloudflare
2. Try to deploy to Cloudflare Pages via `wrangler deploy`

## The current behavior
Uncaught ReferenceError: MessageChannel is not defined

## The expected behavior
Should work in the same way as latest 18 version.

https://github.com/facebook/react/blob/6a4b46cd70d2672bc4be59dcb5b8dede22ed0cef/packages/react-server/src/ReactServerStreamConfigBrowser.js#L16C1-L28C2
