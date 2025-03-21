# [React 19] React compiler strips `await` from `for await` loops

> Issue #29113 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29113

## Description

## Summary

React compiler is compiling

```
async function MyApp({ something }) {
  for await (const deferredState of foo) {
    // do stuff
  }
}
```

into

```
async function MyApp(t0) {
  for (const deferredState of foo) {
  }
}
```

i.e the `for await` became a regular `for`. 

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAQzATwHZwAQBmUuALgJYTZ4CymAggA4MAUwekAtgiQBZnYBzPAF8AlHmAAdKoQgw8aAO5oyJPMziUwagCYICCGDAQ6AyiTQkEeCAVkRxUmXjwB6V3h0R2JKAQLSLsLSwdggwkA


