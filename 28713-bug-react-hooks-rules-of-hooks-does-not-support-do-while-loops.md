# Bug: `react-hooks/rules-of-hooks` does not support `do/while` loops

> Issue #28713 - Created on 4/2/2024

> Original URL: https://github.com/facebook/react/issues/28713

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0

## Steps To Reproduce

1. Use a hook inside a `do/while` loop. 

2. You'll see that it's not considered a violation of the rule.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Code example:

```
function ComponentWithHookInsideDoWhile() {
	do {
		useHookInsideLoop();
	} while (true);
}
```

## The current behavior

The `react-hooks/rules-of-hooks` does not consider hook usage inside a `do/while` loop a violation.

## The expected behavior

I expected that I'd see the following ESLint error:

```
React Hook useHookInsideLoop() may be executed more than once. 
Possibly because it is called in a loop. 
React Hooks must be called in the exact same order in every component render.
```

