# [React 19] Can't use debounce for useCallback -  Expected the first argument to be an inline function expressioneslint(react-compiler/react-compiler)

> Issue #31624 - Created on 11/24/2024

> Original URL: https://github.com/facebook/react/issues/31624

## Description

## Summary

>     "react-compiler-runtime": "19.0.0-beta-0dec889-20241115",
>     "babel-plugin-react-compiler": "19.0.0-beta-0dec889-20241115",
>    "eslint-plugin-react-compiler": "19.0.0-beta-0dec889-20241115",
>     "eslint": "^8.56.0",

.eslintrc.cjs
```cjs
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parser: '@typescript-eslint/parser',
  plugins: ['react-refresh', 'react-compiler'],
  rules: {
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
    "react-compiler/react-compiler": "error"
  },
}

```

I use debounce functoin for fetching api on each input typing, react-compiler eslint error comes out . 
> Expected the first argument to be an inline function expressioneslint(react-compiler/react-compiler)


```ts
  const debouncedSearch = useCallback(debounce(async (query: string) => {
    const response = await fetch(`api/search/quotes?query=${query}`);
      if(response.ok) {
        const { results } = await response.json();
        setResults(results);
      }
      else {
        setResults([]);
      }
  },300),[]);
```
![스크린샷 2024-11-24 오후 11 41 45](https://github.com/user-attachments/assets/06bbcfce-8075-4c30-ae51-2d099b48372e)

how can I pass function be wrapped by another function as a argument in hooks without breaking this lint rule?  Should I just not use `useCallback` in this case?
