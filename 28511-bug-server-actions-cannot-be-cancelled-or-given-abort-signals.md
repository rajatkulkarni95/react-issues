# Bug: server actions cannot be cancelled or given abort signals

> Issue #28511 - Created on 3/7/2024

> Original URL: https://github.com/facebook/react/issues/28511

## Description

React version: 18.2.0

## Steps To Reproduce

1. As in #28510, create a server action that has some long-running delay, e.g.: to simulate a large language model call.
2. There is no API on the client or server to trigger cancellation, or to detect or handle the client navigating away from the page.

Link to code example: https://codesandbox.io/p/devbox/next-14-0-3-forked-7q86s7?file=%2Fapp%2Factions.ts%3A4%2C18&workspaceId=958ee911-ec8f-4ca3-9ce1-668005ecaeb8

## The current behavior

When a long-running request is fired, the server will complete it regardless of client behavior, e.g.: client hangup.

## The expected behavior

An API for server actions to obtain a reference to an AbortController (or similar API) for the request, perhaps via async local context.

An API for clients to signal cancellation of a server action, perhaps via an additional return value on `startTransition`, perhaps as part of the transition APIs. If a transition is explicitly created, there should be a mechanism to cancel it.
