# eslint react-hooks/exhaustive-deps rule should have fine grained ignores

> Issue #27873 - Created on 1/3/2024

> Original URL: https://github.com/facebook/react/issues/27873

## Description

In the exhaustive deps eslint rule, it would be helpful if there was a way to ignore individual dependencies instead of completely disabling the rule.

For example, the following effect is only intended to fire when `shouldRing` changes. And we want to add a log when it calls `playRingtone()` to record the state at the time that it fired.

Right now disabling the rule is the only option:

```ts
const shouldRing = getShouldRing(connectionState, joinState)

useEffect(() => {
  if (shouldRing) {
    log.info('ringing', connectionState, joinState) // it's fine that we don't listen to these
    playRingtone()
    return () => {
      stopRingtone()
    }
  }
// eslint-disable-next-line react-hooks/exhaustive-deps
}, [shouldRing])
```

I can see two alternatives:

- Marking deps as ignored
```ts
useEffect(() => {
  // ...
}, [shouldRing, void connectionState, void joinState])
```
- Marking references as ignored
```ts
// I don't know how well this would work as comments can be hard to associate with the right AST nodes, and tools like eslint/prettier tend to mess with them
log.info('ringing', /* react-hooks/ignore */ connectionState, /* react-hooks/ignore */ joinState)
```

Personally I prefer the former, generally when you want to do this it's because you're actually trying to listen to very specific state/derived values, and for every other dep you'd be marking their changes as not important to the effect.

