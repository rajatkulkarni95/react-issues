# [React 19] Signal & Observable

> Issue #30570 - Created on 8/1/2024

> Original URL: https://github.com/facebook/react/issues/30570

## Description

## Summary

There is huge discussion about Signals and Observables, Solid.js is built upon Signals, highly popular library like `react-use` has `useObservable` util hook.

"Recently", a [Signals proposal](https://github.com/tc39/proposal-signals) appeared and quickly drew attention.

## Proposal

I thought it would be really handy if React would have a way to support this kind of structure - observe the state. I know there is `useSyncExternalStore`, but the signature is a little bit different and it can't be used in conditionals.

So if something like that would work... I would expect the following to work

```tsx
import { use } from "react"
import { searchSignal } from "@/signals"

function Images() {
	const search = use(searchSignal)

	return (...)
}

function App() {
	return (
		<SearchBar />
		<Images />
	)
}

function SearchBar() {
	return <input onChange={event => searchSignal.set(event.currentTarget.value)} />
}
```

## Explanation

The Signal itself is an abstraction, which only implements `get` method and `subscribe` from [this proposal](https://github.com/tc39/proposal-observable).

The `use` hook would have the following signature

```ts
interface Getter<T> {
	get?(): T
}

interface Observable<T> {
	subscribe?(): { unsubscribe(): void }
}

function use<T>(... | Getter<T> | Observable<T> | (Getter<T> & Observable<T>)): T
```

The `Getter` and `Observable` could work in tandem to allow getting initial value while listening for further updates.

---

Not sure about `use`, it might be better to implement completely standalone hook like `useSignal` or `useObservable`.
Not sure if this was already discussed and proposed, I couldn't find any related topics.
