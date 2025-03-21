# Bug: React not defined in TypeScript when importing from npm

> Issue #28822 - Created on 4/11/2024

> Original URL: https://github.com/facebook/react/issues/28822

## Description

React version: all

## Steps To Reproduce
1. Import React from "npm:react" inside Deno
2. Observe that React is not defined in TypeScript

Code example:
```typescript
import * as React from "npm:react";
// here React is not defined in typescript, we need to add @types/react
/* @deno-types="@types/react" */
import * as React from "npm:react";
```

## The current behavior
React is not defined in TypeScript when importing it from "npm:react".

## The expected behavior
React (and react-dom) should ship with types, at least in a .d.mts form, so that users don't have to bother adding types manually. As TypeScript is now widely used, React should provide first-class TypeScript support.

Related issue: https://github.com/denoland/deno/issues/18203 but the solution we have doesn't address the issue directly. Maybe React should ship types and not the @DefinitelyTyped org.
