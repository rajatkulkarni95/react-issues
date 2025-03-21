# [eslint-plugin-react-hooks] Missing type declarations

> Issue #30119 - Created on 6/27/2024

> Original URL: https://github.com/facebook/react/issues/30119

## Description

<ins>Versions:</ins> all

<ins>Severity:</ins> low

## What

When imported in a TypeScript environment, `eslint-plugin-react-hooks` throws a "missing type declarations" error.

![image](https://github.com/facebook/react/assets/28303477/fbb4a4fb-2db6-4d1a-aeba-0e73add1e507)

## Why

This is because `eslint-plugin-react-hooks` does not have any type declarations bundled in the package. These would usually be in an `index.d.ts` file.

Also, `eslint-plugin-react-hooks` does not have a corresponding `@types/...` package in the [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) project for users to rely on.

## Workaround

Users can follow the instructions in the error message and make a temporary module augmentation to declare their own types for the package.

In my personal project, I've done it this way:

```ts
// ./src/@types/eslint-plugin-react-hooks.d.ts
declare module 'eslint-plugin-react-hooks' {
	import type { ESLint } from 'eslint';
	const plugin: Omit<ESLint.Plugin, 'configs'> & {
		// eslint-plugin-react-hooks does not use FlatConfig yet
		configs: Record<string, ESLint.ConfigData>;
	};
	export default plugin;
}
```

But this will not automatically stay up-to-date with the package and is not guaranteed to be correct. Is it also incomplete and does not contain detailed information about the different configs in the plugin.

## How to fix

There are several ways.

1. Usually the preferred solution is just to write everything in TypeScript and let it auto-generate declaration files for you. But I understand if a complete rewrite is not on the table :)

2. You could add a `@types/eslint-plugin-react-hooks` package in the [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) repo. But then your types would be defined in a completely different place from your actual code, and if you ever decide to migrate to TypeScript in the future, the old `@types/...` package would need to be deprecated. Sounds messy.

3. Best solution, in my opinion. Just add a `index.d.ts` file to the package that declare the type exports of the package. Then define it as the type declarations in `package.json`. Easy peasy.

```diff
// package.json
+  "main": "index.js",
+  "types": "index.d.ts",
  "files": [
    "LICENSE",
    "README.md",
    "index.js",
+    "index.d.ts",
    "cjs"
  ],
```

I would be happy to do this myself. I just wanted to submit an issue first to confirm that the maintainers would approve.

## Steps To Reproduce

1. Install `typescript`, `eslint-plugin-react-hooks`
2. Create a `.ts` file
3. Import `eslint-plugin-react-hooks`

## Code example

`package.json`
```json
{
  "scripts": {
    "build": "tsc"
  },
  "dependencies": {
    "eslint-plugin-react-hooks": "^4.6.2"
  },
  "devDependencies": {
    "typescript": "^5.5.2"
  }
}
```

`index.ts`
```ts
import reactHooksPlugin from 'eslint-plugin-react-hooks';
```

(You'll need a `tsconfig.json` file too, but the settings are irrelevant to this example)

## The current behavior

TypeScript build error.

## The expected behavior

No errors.
