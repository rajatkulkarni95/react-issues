# [React 19] React Compiler doesn't preserve HTML Entities

> Issue #29100 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29100

## Description

## Summary

When using React Compiler, this component:
```tsx
export default function MyApp() {
  return <div>Parent &gt; Children</div>;
}
```

becomes

```tsx
function MyApp() {
  const $ = _c(1);

  let t0;

  if ($[0] === Symbol.for("react.memo_cache_sentinel")) {
    t0 = <div>Parent > Children</div>;
    $[0] = t0;
  } else {
    t0 = $[0];
  }

  return t0;
}
```

which leads to this error: `ERROR: The character ">" is not valid inside a JSX element`

Repro: https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvhgJcsNgB5CTAG4A+AApkpdAgDIA5rgDc+AMIALJpUJa5AekWrD4gL7iQzoA

