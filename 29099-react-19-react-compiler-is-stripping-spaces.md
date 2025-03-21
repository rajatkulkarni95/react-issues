# [React 19] React Compiler is stripping spaces

> Issue #29099 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29099

## Description

## Summary

I tested the React Compiler by starting with the Vite React TS Template, updating to React 19 and adding the compiler plugin as described in the docs. With the compiler enabled, the component is missing spaces in some strings (`count is0` and `Editsrc/App.tsx`):

![image](https://github.com/facebook/react/assets/15160542/0f95b219-9e3a-43df-99ed-a80c161278f3)

The relevant code is:

```tsx
<div className="card">
  <button onClick={() => setCount((count) => count + 1)}>
    count is {count}
  </button>
  <p>
    Edit <code>src/App.tsx</code> and save to test HMR
  </p>
</div>
```

Stackblitz: [https://stackblitz.com/edit/vitejs-vite-y8oj4e](https://stackblitz.com/edit/vitejs-vite-y8oj4e?file=vite.config.ts,src%2FApp.tsx&terminal=dev)
