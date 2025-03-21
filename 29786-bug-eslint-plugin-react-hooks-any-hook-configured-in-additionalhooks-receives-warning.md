# Bug: eslint-plugin-react-hooks any hook configured in additionalHooks receives warning

> Issue #29786 - Created on 6/6/2024

> Original URL: https://github.com/facebook/react/issues/29786

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.3.1

## Steps To Reproduce

1. Create a hook, e.g. `function useYada() { return {} as any; }` 
2. Configure eslint `react-hooks/exhaustive-deps` rule with `["warn", { additionalHooks: "(useYada)" }]`.
3. Call the hook e.g. `useYada()` and receive the warning that `React Hook useYada received a function whose dependencies are unknown. Pass an inline function instead`.
4. If you pass ONE argument, no warning is received. If you pass zero or two arguments to the hook, the warning is received.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

Receive a warning that "React Hook useYada received a function whose dependencies are unknown. Pass an inline function instead"

## The expected behavior

No error should be received. No arguments are even being passed to the hook.

## Other notes

Looking at your code, I see that this error comes from a `default:` case in a switch case statement inside of `ExhaustiveDeps > create > visitCallExpression` but I'm not sure what's going on.

I have this code in a private repo, but if you need a reproduction I can spend the time to do that.

Here is my eslint setup:

<details>
  <summary>.eslintrc.cjs</summary>

```js
/** @type {import("eslint").Linter.BaseConfig} */
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-hooks/recommended",
  ],
  ignorePatterns: ["/dist/", "/tmp/", ".eslintrc.cjs"],
  parser: "@typescript-eslint/parser",
  plugins: ["react-refresh"],
  rules: {
    "prefer-const": "warn",
    "@typescript-eslint/ban-types": [
      "warn",
      {
        // See https://github.com/typescript-eslint/typescript-eslint/issues/2063#issuecomment-675156492
        extendDefaults: true,
        types: {
          "{}": false,
        },
      },
    ],
    "@typescript-eslint/explicit-function-return-type": "off",
    // "@typescript-eslint/naming-convention": "warn",
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-namespace": "off",
    // "@typescript-eslint/no-non-null-assertion": "off",
    "@typescript-eslint/no-use-before-define": "off",
    "@typescript-eslint/no-unused-vars": [
      "warn",
      {
        /** Allow all unused args. */
        argsIgnorePattern: ".",
        /** Allow unused vars that start with an underscore. */
        varsIgnorePattern: "^_",
      },
    ],
    // "@typescript-eslint/no-var-requires": "off",
    "react-hooks/exhaustive-deps": [
      "warn",
      {
        additionalHooks: "(useYada|usePlatform|useWorkbench)",
        // stableHooksPattern: "usePlatform|useWorkbench",
      },
    ],
    "react-refresh/only-export-components": [
      "warn",
      { allowConstantExport: true },
    ],
  },
  overrides: [
    {
      files: ["**/*.{md,mdx}"],
      extends: ["plugin:mdx/recommended"],
      parser: "eslint-mdx",
      parserOptions: {
        project: "./tsconfig.json",
        ecmaFeatures: {
          jsx: true,
        },
        ecmaVersion: 12,
        sourceType: "module",
        extraFileExtensions: [".mdx"],
        extensions: [".mdx"],
      },
      // optional, if you want to lint code blocks at the same time
      settings: {
        "mdx/code-blocks": true,
        // optional, if you want to disable language mapper, set it to `false`
        // if you want to override the default language mapper inside, you can provide your own
        "mdx/language-mapper": {},
      },
    },
  ],
};
```

</details>

