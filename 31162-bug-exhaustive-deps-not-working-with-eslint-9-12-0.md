# Bug: exhaustive-deps not working with eslint 9.12.0

> Issue #31162 - Created on 10/10/2024

> Original URL: https://github.com/facebook/react/issues/31162

## Description

Here is a simplified version of my `eslint.config.mjs`: 
(There are a lot more rules, custom plugins, ignores, files specifications, etc. but for the sake of this bug, I think this will do)

```js
import tseslint from 'typescript-eslint';
import reactHooks from 'eslint-plugin-react-hooks';
import { fixupPluginRules } from '@eslint/compat';

export default tseslint.config({
  plugins: {
    'react-hooks': fixupPluginRules(reactHooks),
  },
  rules: {
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'error',
});
```

Here are the versions that I am running:

```
yarn list eslint eslint-plugin-react-hooks typescript-eslint

yarn list v1.22.19
warning Filtering by arguments is deprecated. Please use the pattern option instead.
├─ eslint-plugin-react-hooks@4.6.2
├─ eslint@9.12.0
└─ typescript-eslint@8.8.1
Done in 0.42s.
```

If I attempt to run `yarn eslint` without `fixupPluginRules` I get the following error:

```
Oops! Something went wrong! :(

ESLint: 9.12.0

TypeError: context.getSource is not a function
Occurred while linting FILE (this is a placeholder)
Rule: "react-hooks/exhaustive-deps"
```

When I run `yarn lint` with `fixupPluginRules` it works fine.

If found the solution to this here: https://eslint.org/docs/latest/use/troubleshooting/v9-rule-api-changes
That eslint documentation explicitly states that if fixupPluginRules is required, I should open an issue on the plugin
![image](https://github.com/user-attachments/assets/43581bb8-1a4e-4e5a-80e8-1b6a87d87950)


