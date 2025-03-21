# Bug: Expected Static Flag Was Missing 

> Issue #29914 - Created on 6/16/2024

> Original URL: https://github.com/facebook/react/issues/29914

## Description

I have a Server Side Rendered React app I'm using Bun to run. Something about the state of my form is causing a static flag was missing error. I dont notice any problems in my application as of now. I am writing this since it says please notify the React team in the error log

```
GamePageIndex.1718554801619.js:227  Warning: Internal React error: Expected static flag was missing. Please notify the React team.
    at HP (http://localhost:3000/indexes/GamePageIndex.1718554801619.js:349:29726)
    at div
    at CP (http://localhost:3000/indexes/GamePageIndex.1718554801619.js:349:31993)
    at div
    at main
    at body
    at html
    at LP (http://localhost:3000/indexes/GamePageIndex.1718554801619.js:349:32856)
```

and in the index file the error points to this (bundled) code 

```
console.error = function() {
    const c = [...arguments].join("");
    if ((c == null ? void 0 : c.startsWith("Warning:")) && c.includes("useContext")) {
        console.error = lI;
        return
    }
    return lI.apply(this, arguments) // Error on this line
}
;
```

React version: 18.3.1

## Steps To Reproduce

1. Build a TSX component that contains the html tag as the outermost tag and then in the body create a form tag that uses react useState to control changes
2. Server Side render these pages using Bun and Elysia
3. I dont know how to reproduce the bug further than this it just appeared in the midst of me coding with no real information on it hence i think it might just be a regression


Link to code example:

I can not provide an example at this time only reporting because it says to in the error log so i figured you would like to know

## The current behavior


## The expected behavior

