# [React 19] Support React Compiler with older React versions for libraries

> Issue #29111 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29111

## Description

@poteto asked me to create this issue for discussion.

It would be useful for library authors if the React Compiler could work with older versions of React. Libraries often need to support many different versions of React to avoid breaking older applications that haven't had a chance to update yet. That's the case for us with React Aria, which supports 16.8+. We can't really release a major version that bumps the requirement to React 19 because we have to support many older applications still using 16-18 that haven't prioritized updating yet. We can't realistically leave those applications behind, or maintain multiple major versions of React Aria ourselves, which means we can't use the compiler.

It would be amazing if the compiler could optionally generate regular `useMemo`, or there was a shim available for older versions of React (similar to the `useSyncExternalStore` shim that was previously released). This could be available specifically for library authors who need to support multiple versions of React, rather than applications (which should just update to React 19).
