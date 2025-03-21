# [React 19] Suspense fallback shows for too long compared to v18

> Issue #31697 - Created on 12/8/2024

> Original URL: https://github.com/facebook/react/issues/31697

## Description

## Summary
In React 19, a ```Suspense``` fallback always seems to show for a minimum of a few hundred ms even after a promise has resolved.

I'm unsure if this is a bug, or expected behaviour with the changes to ```Suspense``` in React 19, but I noticed this when trying out the 19 beta a few months ago on an app that makes use of ```Suspense``` a lot (Relay) and it felt as if the app was being throttled to use 4g due to the delay in the fallback being hidden and the children rendered even after the network request had finished. This was especially perceptible when loading a query on user action, e.g hover. 

# Reproduction
See the videos and links below for a minimal reproduction. Note how in 18, the fallback is barely a flicker, whereas in 19 the fallback is visible for a few hundred ms.

[React 19 Codesandbox](https://codesandbox.io/p/sandbox/react-19-suspense-repro-88xlkj)
[React 18 Codesandbox](https://codesandbox.io/p/sandbox/react-18-suspense-clv3td)

## React 18.2.0 (expected behaviour)

https://github.com/user-attachments/assets/47b77675-5c22-439e-9cab-16f9f85242a0

## React 19.0 
https://github.com/user-attachments/assets/63603f1c-82f5-4448-b2b8-93ccd33bc23d


