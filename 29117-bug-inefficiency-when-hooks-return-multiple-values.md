# Bug: Inefficiency when hooks return multiple values

> Issue #29117 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29117

## Description

React compiler inefficiently re-evaluates code when dependencies that do not affect the result have changed. Specifically, when the hook returns multiple values.

Input code:

```ts
export default function Test() {
  const [data, refetch] = useData();

  const y = deepClone(data);

  return (
    <div>
      <button onClick={refetch}>
        Refetch
      </button>
      <span>
        {JSON.stringify(y)}
      </span>
    </div>
  );
}

```

[Check the output JS here - Link to Playground](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwBUExcAKASnzAAOm3xxW3fAG1CZXGQA0+GKQS44ACwC6+ALz4oYBABE5ZfgG4RI-GIkEAnnqIIEmAMKVWCHrPl9rURVcWDYeG1t8AB5CJgA3AD4IyOiAIyhcXFZ8Vk8mOABrXWAVEjVNAF8k0RTbACVVdQ1kyKiAenTM1mra6LBMMjoe3sEAKQBlAHkAOQA6bhgmOgBzJhIHHgc+Cpbbdv7B4b222MSIvis6CpAKoA
)

## Steps To Reproduce

1. Use the provided original code in a React component.
2. Observe the generated code by the React compiler.
3. Note that `deepClone(data)` is re-evaluated when refetch changes.

Check the playground link above ^

## The current behavior

- The line const `y = deepClone(data);` is re-evaluated whenever refetch changes, even if data remains the same.
- This inefficiency arises because the compiler does not memoize `y` independently from other variables like `t1`.

## The expected behavior

`y` should be memoized separately to avoid re-computation when only refetch changes and data remains the same.

