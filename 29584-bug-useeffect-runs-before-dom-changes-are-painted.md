# Bug: useEffect runs before DOM changes are painted

> Issue #29584 - Created on 5/24/2024

> Original URL: https://github.com/facebook/react/issues/29584

## Description

React version: ^18.0.0

## Steps To Reproduce

1. Refer the attached [codesandbox link](https://codesandbox.io/p/sandbox/tic-tac-toe-gpjn57) 
2. Consider the click that leads to a winner in tic-tac-toe game
3. We get an alert that a player has won, however, the board is not yet painted on the browser.
4. The expectation of browser painting the click first followed by the effect execution is broken.

Video Link explaining the bug: 
[https://www.youtube.com/watch?v=v8KLOx_Mm48](https://www.youtube.com/watch?v=v8KLOx_Mm48) 

Link to code example:
[https://codesandbox.io/p/sandbox/tic-tac-toe-gpjn57](https://codesandbox.io/p/sandbox/tic-tac-toe-gpjn57)


## The current behavior
The expectation of browser painting the click first followed by the effect execution is broken.
We get an alert first, then the updated board is painted by browser.

## The expected behavior
We expect the board to update first, then the effect should run which should cause the alert.
