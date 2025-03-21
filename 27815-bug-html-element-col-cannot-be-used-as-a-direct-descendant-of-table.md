# Bug: HTML element <col> cannot be used as a direct descendant of <table>

> Issue #27815 - Created on 12/8/2023

> Original URL: https://github.com/facebook/react/issues/27815

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: * <= 18.2.0

## Steps To Reproduce

1. Have a `table` element with a `col` element as a direct descendant, outside of a `colgroup` 
2. See the console error: `Warning: validateDOMNesting(...): <col> cannot appear as a child of <table>.`

<img width="1006" alt="Screenshot 2023-12-08 at 14 40 04" src="https://github.com/facebook/react/assets/9933592/83e81439-ae5f-414b-aeea-89be71022d39">

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://jsfiddle.net/yz0jdt9a/

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

The `validateDOMNesting` function currently identifies the `col` element as an invalid child of `table`, and expects that the input instead be wrapped in a `colgroup` element.

i.e.

Currently indicated as invalid:
```
<table>
  <col>
  <col>
  <thead>
    ...
```

Current behavior understood as valid.
```
<table>
  <colgroup>
    <col>
    <col>
  </colgroup>
  <thead>
    ...
```

## The expected behavior

The [HTML spec](https://html.spec.whatwg.org/multipage/tables.html#the-colgroup-element) for the `colgroup` element identifies that

> A [colgroup](https://html.spec.whatwg.org/multipage/tables.html#the-colgroup-element) element's [start tag](https://html.spec.whatwg.org/multipage/syntax.html#syntax-start-tag) can be omitted if the first thing inside the [colgroup](https://html.spec.whatwg.org/multipage/tables.html#the-colgroup-element) element is a [col](https://html.spec.whatwg.org/multipage/tables.html#the-col-element) element, and if the element is not immediately preceded by another [colgroup](https://html.spec.whatwg.org/multipage/tables.html#the-colgroup-element) element whose [end tag](https://html.spec.whatwg.org/multipage/syntax.html#syntax-end-tag) has been omitted. (It can't be omitted if the element is empty.)

Similarly the [MDN docs](https://developer.mozilla.org/en-US/docs/web/html/element/col) for `col` specifies under the "Permitted Parents" heading

>  parents | `colgroup` only, though it can be implicitly defined as its start tag is not mandatory. The `colgroup` must not have a span attribute.

To that end, the table element should accept `col` as a valid nested element.


