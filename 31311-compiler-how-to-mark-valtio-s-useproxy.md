# [Compiler]: How to mark valtio's `useProxy`

> Issue #31311 - Created on 10/21/2024

> Original URL: https://github.com/facebook/react/issues/31311

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [X] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://github.com/nmay231/eslint-plugin-react-compiler-bug

### Repro steps

How to see issue with given repo:
1. Clone repo above.
2. Click the optimized button 5+ times. The child component stops rerendering since the prop no longer changes
3. Click the unoptimized button 5+ times. The child component keeps rerendering even though the function is safe to memoize.

When you pass a [valtio](https://github.com/pmndrs/valtio) proxy object to `useProxy`, it is safe to modify the resulting proxy object directly as a way to `setState`. Peeking at `Unoptimized.tsx`, in particular the button `onClick` handler:

```tsx
export function Unoptimized() {
    const state = useProxy(stateProxy)
    return (
        <>
            <p>Unoptimized</p>

            {/* Child continues to rerender even though props are the same */}
            <ChildComponent clicks={Math.min(state.clicks, 5)} />

            <button
                onClick={() => {
                    // Lint error: Mutating a value returned from a function whose return value should not be mutated
                    state.attr = !state.attr
                    stateProxy.clicks += 1
                    console.log(stateProxy.clicks)
                }}>
                Clicked {state.clicks}
            </button>
        </>
    )
}
```

## The problem

The compiler (and eslint plugin) fail to realize this is safe to optimize, aka this is a false negative. One workaround is to use `const state = useSnapshot(myProxy)` for reading from the proxy and to modify the proxy object directly (`myProxy.attr = ...`). Another is to manually optimize with `React.memo` where proxy objects are used, but that feels counter-productive.

The real question is, **Is there a way for valtio developers to mark `useProxy`'s return value as safe to mutate?**

Thanks.

<details>

<summary>
Steps to recreate repo from scratch
</summary>

1. `pnpm create vite`
4. `pnpm add -D eslint-plugin-react-compiler@beta`
5. `pnpm add react-compiler-runtime@beta babel-plugin-react-compiler@beta valtio`
6. Update eslint config to use plugin, and `vite.config.ts` to use babel plugin (skimming though [this guide](https://jherr2020.medium.com/react-compiler-with-react-18-1e39f60ae71a) helped me).
7. Create a proxy object, and use the proxy object using valtio's `useProxy` hook.
8. Modifying the proxy object should be safe to do, but the compiler rules are too simple to realize that it is safe.

</details>

### How often does this bug happen?

Every time

### What version of React are you using?

18.3.1

### What version of React Compiler are you using?

19.0.0-beta-8a03594-20241020
