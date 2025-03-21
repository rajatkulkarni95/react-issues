# [React 19] `eslint-plugin-react-compiler` throws SyntaxErrors when it encounters `.json` or `.graphql` files

> Issue #29107 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29107

## Description

## Summary

If your linting command encompasses `.json` or `.graphql` files (e.g. `eslint . package.json --ext .js,.jsx,.ts,.tsx,.graphql`), and you have react-compiler/react-compiler enabled in your rules object:

```
  rules: {
    'react-compiler/react-compiler': 'error',
```

Then HermesParser will throw an exception and stop linting:

```
SyntaxError: Error while loading rule 'react-compiler/react-compiler': ';' expected (1:6)
query MemberProfile($id: ID!) {
      ^
```

This is the stack trace for the error:

```
Occurred while linting /<obfuscated>/app/scripts/controller/MemberProfileQuery.graphql
    at Object.parse (/<obfuscated>/web/node_modules/hermes-parser/dist/HermesParser.js:91:29)
    at Object.parse (/<obfuscated>/web/node_modules/hermes-parser/dist/index.js:129:28)
    at Object.create (/<obfuscated>/web/node_modules/eslint-plugin-react-compiler/dist/index.js:69121:42)
    at createRuleListeners (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:895:21)
    at /<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:1066:110
    at Array.forEach (<anonymous>)
    at runRules (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:1003:34)
    at Linter._verifyWithoutProcessors (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:1355:31)
    at Linter._verifyWithConfigArray (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:1807:21)
    at Linter.verify (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:1437:65)
    at Linter.verifyAndFix (/<obfuscated>/web/node_modules/eslint/lib/linter/linter.js:2068:29)
    at verifyText (/<obfuscated>/web/node_modules/eslint/lib/cli-engine/cli-engine.js:254:48)
    at CLIEngine.executeOnFiles (/<obfuscated>/web/node_modules/eslint/lib/cli-engine/cli-engine.js:834:28)
    at ESLint.lintFiles (/<obfuscated>/web/node_modules/eslint/lib/eslint/eslint.js:551:23)
    at Object.execute (/<obfuscated>/web/node_modules/eslint/lib/cli.js:421:36)
    at async main (/<obfuscated>/web/node_modules/eslint/bin/eslint.js:152:22)
```

The workaround to solve this right now is to disable the rule for these files using an override:

```
  overrides: [
    {
      files: ['*.json'],
      rules: {
        'react-compiler/react-compiler': 'off',
      },
    },
    {
      files: ['*.graphql'],
      rules: {
        'react-compiler/react-compiler': 'off',
      }
    }
  ]
```
