# [Compiler Bug]: Mutating a ref passed as argument from a hook warns

> Issue #29832 - Created on 6/10/2024

> Original URL: https://github.com/facebook/react/issues/29832

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhASwLYAcIwC4AEAVAQIZgEBKCpchAZjBBgQOQw12sDcAOgHYCEADxz4C9KPzpoI-AlDAJqYNAC8EACVL8AJgBsEACgEECeUjADmCPMiqc8AOgCyUCwCND1egHkPAFYIdAA8mgAqLgAyACJoAG4AooYYCPyEAD4E-FD6+gB8ADQCAJQEwKYEcHJghB6WBAC8DrTOisoI9GGRsQnJCKnp+UY5eSV8gvItdE7tifT0wXhGRmWN+eWVZpLSeLLyHKoa-kF0RgjxaXYELtBKiZfpBFnh0HAAFg9XZRVTZmb1GBOOCwDjpJy1ACehicAHc0Lo8O8mgReCAAIwABiwwjRE3+-ws1lswNBVwheGhCDhCKRKLRWJxeK2BAAvgIWboICDBs5SLpdF90lE0LU0ggYEZWBg7gMIJdWIUCId1AgTkslcACFhyKpLvZ6KR9Eo2eMWRw8LB5KsmhtfgSzFyeeSODLLkK8CKxfwJVKZe03QhFcqEEc1YElma-mz8WylQBtIk2PAAXSjZgtVs20d0MFIVisaH4VnseBgUAQxSmrIm7P4IFZQA

### Repro steps

```jsx
import * as React from 'react';

export function useResizeHandle(
  target: React.MutableRefObject<HTMLDivElement | null>,
) {
  const bar = React.useRef<HTMLDivElement>(null);

  React.useEffect(() => {
    function resizeObject(event: MouseEvent | TouchEvent) {
      bar.current.style.width = "10px";
      target.current.style.width = "10px";
// ~~ InvalidReact: Mutating component props or hook arguments is not allowed. Consider using a local variable instead. Found mutation of `target`
    }

    document.addEventListener('mousemove', resizeObject, { passive: false });
    return () => {
      document.removeEventListener('mousemove', resizeObject);
    };
  }, [target]);
  return {
    dragging: true,
  };
}
```

This seems like the same as #29196 but in reverse.

From what @josephsavona said:

> we will likely need to explore a heuristic for understanding which values may be refs, based on the ecosystem convention of "ref" or "-Ref".

This could make sense. I could see myself doing:

```diff
 export function useResizeHandle(
-  target: React.MutableRefObject<HTMLDivElement | null>,
+  targetRef: React.MutableRefObject<HTMLDivElement | null>,
 ) {
```

### How often does this bug happen?

Every time

### What version of React are you using?

v19
