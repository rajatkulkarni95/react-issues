# Bug: eslint-plugin-react-hooks hangs on function with many conditionals

> Issue #28167 - Created on 2/1/2024

> Original URL: https://github.com/facebook/react/issues/28167

## Description

~React~ eslint-plugin-react-hooks version: 4.6.0

## Steps To Reproduce

1. Write a function with a bunch of conditionals, and a React hook.
2. Run the rules-of-hooks linter. (For example, add an eslint config like `{ rules: { "react-hooks/rules-of-hooks": "error" } }`.)

<details><summary>Code example</summary>

```
function useFoo() {}
function f(x: number[], y: number, b: boolean) {
	if (y === 3) {
		return
	}
	let z
	for (const i of x) {
		if (i === 0) {
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
			z = b ? i : y
		} else if (i === 1) {
			useFoo()
		}
	}
}
```

</details>

## The current behavior

Linter spins forever, eventually runs out of memory, etc. Specifically, it's spinning in `countPathsFromStart`, which seems to be computing all possible paths through the control-flow graph to the hook. (I think it's doing it somewhat inefficiently, although that's probably beside the point.) With a smaller, but still large, number of conditionals it eventually reports:
```
error: React Hook "useFoo" is called in function "f" that is neither a React function component nor a custom React Hook function. React component names must start with an uppercase letter. React Hook names must start with the word "use" (react-hooks/rules-of-hooks) at tmp.ts:32:4:
```

## The expected behavior

This hooks usage is obviously wrong! We shouldn't need to compute the exact number of paths to know that; as soon as you have an early return before the hook, or a hook inside a loop, we should be able to say that's wrong. Indeed, the lint error isn't even related to any of that, we get it just from the name of the containing function.

Obviously this is garbage code. But it's simplified from a real issue that a colleague ran into:
- We had a function with a ton of conditionals (a for, with a large multi-branched if, where some of the branches had many cases within, many of them via ternaries/optional-chaining/etc. which can easily add up).
- They added a call, deep inside one of those cases, to a function with a hook-style name (it wasn't actually a hook, and the function wasn't actually a component, nor was it even named like a component).
- eslint spun for a while then ran out of memory.
In this case it wasn't at all obvious what was at issue. Once we tracked down that the problem was the hooks linter, it was very easy to fix! (Simply name the function something else. In this case we could probably also exclude the file from the linter -- it has no React components -- but many sibling files do so it easily could have happened in a file with components.) But we didn't even realize that this name was not kosher, because we never got to the lint error, or even knew what linter was stuck, until we did a binary search on our whole eslint config.

Instead, the linter could one or more of the following:
- Skip the analysis if the nearest containing function doesn't look like a component.
- Early-out from the analysis if the numbers get too large, and return an error like "this function's control-flow was too complex to analyze, probably don't use hooks".
- Do the analysis more efficiently (e.g. notice cases where there are a fixed number of branches, and do some combinatorics instead of traversing all paths); this is probably harder but might allow avoiding even small behavior changes.
