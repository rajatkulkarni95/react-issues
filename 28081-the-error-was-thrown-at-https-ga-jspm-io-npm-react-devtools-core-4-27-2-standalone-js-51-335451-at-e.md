# The error was thrown at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:335451     at ee.emit (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:281929)     at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:283476     at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679409     at Array.forEach (<anonymous>)     at Am.$.onmessage (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679392)[DevTools Bug] Cannot add node "1" because a node with that id is already in the Store.

> Issue #28081 - Created on 1/25/2024

> Original URL: https://github.com/facebook/react/issues/28081

## Description

### Website or app

localhost

### Repro steps

The error was thrown at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:335451
    at ee.emit (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:281929)
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:283476
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679409
    at Array.forEach (<anonymous>)
    at Am.$.onmessage (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679392)

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-core

### DevTools version (automated)

4.27.2-7f747b80e

### Error message (automated)

Cannot add node "1" because a node with that id is already in the Store.

### Error call stack (automated)

```text
at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:335451
    at ee.emit (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:281929)
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:283476
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679409
    at Array.forEach (<anonymous>)
    at Am.$.onmessage (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679392)
```


### Error component stack (automated)

```text
The error was thrown at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:335451
    at ee.emit (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:281929)
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:283476
    at https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679409
    at Array.forEach (<anonymous>)
    at Am.$.onmessage (https://ga.jspm.io/npm:react-devtools-core@4.27.2/standalone.js:51:679392)
```


### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot add node  because a node with that id is already in the Store. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

