# Bug: in chrome version  127.0.6533.100 and the previous release, debugger hangs on breakpoint, when attempting to interact with values

> Issue #30664 - Created on 8/12/2024

> Original URL: https://github.com/facebook/react/issues/30664

## Description

Starting with the version ending in .88 and in  127.0.6533.100, the react devtool plugin hangs when a breakpoint is hit and you attempt to hover over any variables in the current scope, where the break happened.   You can briefly scroll the right panel with the mouse wheel, but fairly soon that goes away too.  If you immediately press continue, the code continues to run.  Otherwise, you have to press F12 to remove the debugger and press F12 again to restart it.  The other tabs seem to function normally, but the ability to set breakpoints and inspect elements is very broken


React version:
Extension 5.3.1, react 17.02

## Steps To Reproduce

1. Set a breakpoint
2. Reach the breakpoint.
3. Attempt to inspect elements  in the current scope.
4. Find the debugger is now hung and will not interact with the mouse.

I don't have a code example, it doesn't seem to be dependent on any particular code, it behaves the same in every part of our application; set a breakpoint, hit it, and you are stuck.


## The current behavior
Debugger hangs upon stopping at a breakpoint

## The expected behavior
Debugger allows user to inspect code and variables when hitting a breakpoint.
