# Bug: React DOM's renderToPipeableStream generates HTML that breaks §13.2.6.3 of the HTML standard

> Issue #32076 - Created on 1/15/2025

> Original URL: https://github.com/facebook/react/issues/32076

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0.0

## Steps To Reproduce

1. Clone code example below
2. Run with `npm start` or `tsx .`
3. Open http://localhost:3000
4. See rendering different from actual HTML

Link to code example: https://github.com/gabrielmfern/reproduction-implied-end-tags-react-ssr

## The current behavior

HTML currently gets rendered in a way that can be considered as invalid per what is described [here](https://html.spec.whatwg.org/multipage/parsing.html#closing-elements-that-have-implied-end-tags) in the HTML standard. This can cause issues for parsing the HTML before getting it to the browser, and it can also lead to unexpected behavior when in the browser.

Here's the freshly-rendered HTML:

```html
<p>
  First
  <div>...</div>
  Text in between paragraphs
</p>
```
<!-- The above </p> doesn't even get properly highlighted on GitHub either -->

Here's the HTML after getting into Chromium:

```html
<p>
  First
</p>
<div>...</div>
Text in between paragraphs
<p></p>
```

## The expected behavior

That React itself would render an output as close to the HTML on the browser as possible. Or, a bit less opinionated stance, would be to at least expect valid, in the sense of the standard, HTML.
