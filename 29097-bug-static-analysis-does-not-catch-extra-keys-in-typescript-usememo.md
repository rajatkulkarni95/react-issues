# Bug: Static Analysis Does Not Catch Extra Keys in TypeScript useMemo

> Issue #29097 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29097

## Description

React version: 18.0.0

### Steps To Reproduce

In the following code, the issue arises where "Extra keys that do not exist in the type do not trigger a static analysis error."

```typescript
import React from 'react';

type Sample = {
  a: string;
  b: number;
};

export default function App() {
  const sample = React.useMemo<Sample>(() => {
    return {
      a: '1',
      b: 1,
      c: '1', // <- Does not exist in Sample, but no static analysis error
      d: 2, // <- Does not exist in Sample, but no static analysis error
      e: {
        // <- Does not exist in Sample, but no static analysis error
        f: 'g', // <- Does not exist in Sample, but no static analysis error
      },
    };
  }, []);

  return null;
}
```

Link to code example: [playcode.io/1872500](https://playcode.io/1872500)

### Current Behavior

No type errors occur.

### Expected Behavior

Type errors should occur for keys c, d, and e which do not exist in the type definition.
