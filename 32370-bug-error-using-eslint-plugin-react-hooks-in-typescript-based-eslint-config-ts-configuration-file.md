# Bug: Error using eslint-plugin-react-hooks in TypeScript-based eslint.config.ts configuration file

> Issue #32370 - Created on 2/13/2025

> Original URL: https://github.com/facebook/react/issues/32370

## Description

Importing eslint-plugin-react-hooks into a TypeScript source file generates the following error:

```
TS7016: Could not find a declaration file for module eslint-plugin-react-hooks.
```

Similarly, adding the plugin generates the following ESLint error:

```
ESLint: Unsafe assignment of an error typed value. (@typescript-eslint/ no-unsafe-assignment)
```

React version: N/A

## Steps To Reproduce

Create an ESLint configuration file in TypeScript format using the typescript-eslint package per below. Note the @ts-expect-error and eslint-disable-next-line directives.

```typescript
import { esLintConfigAIDCToolkit } from "@aidc-toolkit/dev";
import type { TSESLint } from "@typescript-eslint/utils";
// @ts-expect-error -- No .d.ts file available.
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import globals from "globals";
import tseslint from "typescript-eslint";

export default tseslint.config(
    ...esLintConfigAIDCToolkit,
    {
        languageOptions: {
            globals: globals.browser
        },
        plugins: {
            // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment -- No .d.ts file available.
            "react-hooks": reactHooks,
            "react-refresh": reactRefresh
        },
        rules: {
            "no-alert": "off",
            "no-console": "off",

            // eslint-disable-next-line @typescript-eslint/no-unsafe-type-assertion,@typescript-eslint/no-unsafe-member-access -- No .d.ts file available.
            ...(reactHooks.configs.recommended.rules as Record<string, TSESLint.FlatConfig.RuleEntry>),
            "react-refresh/only-export-components": [
                "warn",
                {
                    allowConstantExport: true
                }
            ],
            "@stylistic/jsx-closing-bracket-location": "off",
            "@stylistic/jsx-closing-tag-location": "off",
            "@stylistic/jsx-curly-spacing": [
                "error",
                {
                    when: "never",
                    children: true
                }
            ],
            "@stylistic/jsx-indent-props": ["error", 4],
            "@stylistic/jsx-wrap-multilines": "off"
        }
    }
);
```

Link to code example:

https://github.com/aidc-toolkit/demo/blob/f81f08348e9d9aaa72206738d22fbc45a19dced2/eslint.config.js

Rename the above to eslint.config.ts to trigger the errors.

## The current behavior

Compiler error on import, ESLint error on plugin declaration.

## The expected behavior

No errors.
