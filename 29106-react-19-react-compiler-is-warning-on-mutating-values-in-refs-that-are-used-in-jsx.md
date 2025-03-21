# [React 19] React compiler is warning on mutating values in refs that are used in JSX.

> Issue #29106 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29106

## Description

## Summary

When mutating a ref value in an event handler (e.g. when dealing with uncontrolled inputs), the React Compiler ESLint rule is giving the following error:

ESLint: Updating a value used previously in JSX is not allowed. Consider moving the mutation before the JSX(react-compiler/react-compiler)

Linked CodeSandbox:

https://codesandbox.io/p/sandbox/kind-mirzakhani-qzw4t3

Linked Compiler Playground:

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswNJpQQBJOpii4ASqXwBefFDAINJfAB58ACQAq7ADJKVuAKLyAtgjoEAPvjpVK+AHz4-D6UlIIA3OLi+JLSBAAWZHSE8gDKUABGzkwEOvwIAG5uuMj4GmSMAHQAYjjODkXuxpY2tTD1LsX+wlqBYhIxhcWVmDBD7gAipBTUQpF00TH4TEb8JHKKyqqGlXCwY+74AGRH+Ovydtuku-vD5whgwv1LS1J0Mmcb2p8XW+rXexgB1wlXuYAA2gAGAC68xeMTekHklUoEAA5msNhFFi97pd-iQbkDhgUyJQoAhvqIQNS4UsAL6LenzRZjXCwNj8HEmEh1fCsdJZHJaYCJZJpTLZXD0-zcmLGJh-fC4TiYBBaan3an4MYkEV4v6Gen4AD0soGS2MGVUuFYytV6upYElOWp-kFUuMJutuFtdHNLy9vPaAfw2LojLoIHpQA

This feels slightly wrong to me as the docs specifically call out manipulating the DOM with a ref as a pattern:
https://react.dev/reference/react/useRef#manipulating-the-dom-with-a-ref

I guess this is because you can do unsafe changes to refs but might be better off as a warning rather than an error?
