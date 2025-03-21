# Feature Request: useOnLoadEffect() -> empty dependency array useEffect wrapper

> Issue #28866 - Created on 4/18/2024

> Original URL: https://github.com/facebook/react/issues/28866

## Description

Currently React requires an empty dependency array to use an effect only on components' initial render.

This frequently causes confusion for new React developers that could be remedied with the addition of a unique named hook that handles this case. Adheres to a design principle that says "_Names should specify their intent, if a function or variable requires documentation then its name does not specify its intent_".

```ts
// Requires the developer to know what this does either through prior trial and error, or prior learning.
// Often mistakenly interpreted by new developers as an effect that will run every render.
useEffect(() => {

}, [])

// Name provides the intent. Developer can interpret behavior without framework specific knowledge.
useOnLoadEffect(() => {

});
```

This could provide clarity for React applications. Upon implementation, could potentially provide hinting to use the new hook when an empty array is detected to remain backwards compatible. Same logic could be applied for useMemo.

```ts
useOnLoadMemo(() => {

});
```


