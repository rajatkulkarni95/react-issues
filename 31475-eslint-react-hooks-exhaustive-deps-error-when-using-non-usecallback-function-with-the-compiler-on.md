# ESLint `react-hooks/exhaustive-deps` error when using non-`useCallback` function with the compiler on

> Issue #31475 - Created on 11/11/2024

> Original URL: https://github.com/facebook/react/issues/31475

## Description

The internet doesn't have much information about the compiler yet so I couldn't find an answer to this. I assume react compiler will simply memoize the functions declared inside the components like `useCallback`. Am I right?

If this is the case, there shouldn't be a need for this warning/error: `The 'fn' function makes the dependencies of useEffect Hook (at line xx) change on every render. Move it inside the useEffect callback. Alternatively, wrap the definition of 'fn' in its own useCallback() Hook.`

Is the `react-hooks` plugin conflicting with the compiler? Should we remove this plugin if we're using the compiler eslint plugin? Or is the warning actually right about this?
