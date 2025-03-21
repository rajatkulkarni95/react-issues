# Bug: React overwrites functions on customElements

> Issue #31689 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31689

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0.0

## Steps To Reproduce

1. Define a custom element as shown:
```js
class CEWithAttrPropertyClash extends HTMLElement {
    test(value) {
        this.dispatchEvent(new CustomEvent('test', {detail: value}))
    }
    connectedCallback() {
        this.test(true);
    }
}

customElements.define('ce-with-attr-property-clash', CEWithAttrPropertyClash);
```
2. Render
```js
render(<ce-with-attr-property-clash test />);
```

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codesandbox.io/p/sandbox/green-resonance-kpwcqg?file=%2Fsrc%2FApp.js%3A10%2C1

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

```this.test is not a function```


## The expected behavior

React sets attribute as an attribute and does not override function definition

The culprit appears to be this line: https://github.com/facebook/react/blob/c56c6234328a29930487295afe61597db48f058c/packages/react-dom-bindings/src/client/DOMPropertyOperations.js#L220

Which does not check to see if the property is a settable property.

