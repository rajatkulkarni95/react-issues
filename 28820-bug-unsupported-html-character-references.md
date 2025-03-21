# Bug: Unsupported HTML character references

> Issue #28820 - Created on 4/11/2024

> Original URL: https://github.com/facebook/react/issues/28820

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React does not support all the named character references, “entities”, defined in the HTML specification:
- Table: https://html.spec.whatwg.org/multipage/named-characters.html#named-character-references
- JSON: https://html.spec.whatwg.org/entities.json

React version: 18.2.0

## Steps To Reproduce

Render the following demo component and compare the exepcteds character and the actual rendering results.

<details>
<summary>Code demo</summary>

```jsx
const HTMLCharRefDemo = () => (
  <>
    <h1>Test: HTML character references in React</h1>
    <table>
      <thead>
        <tr>
          <th>Reference</th>
          <th>Expected character</th>
          <th>Actual rendering</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>&amp;copy;</td>
          <td>©</td>
          <td>&copy;</td>
        </tr>
        <tr>
          <td>&amp;bemptyv;</td>
          <td>⦰</td>
          <td>&bemptyv;</td>
        </tr>
        <tr>
          <td>&amp;check;</td>
          <td>✓</td>
          <td>&check;</td>
        </tr>
        <tr>
          <td>&amp;bigstar;</td>
          <td>★</td>
          <td>&bigstar;</td>
        </tr>
        <tr>
          <td>&amp;NoBreak;</td>
          <td>{'\u2060'}</td>
          <td>&NoBreak;</td>
        </tr>
      </tbody>
    </table>
  </>
);
```

</details>

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://codepen.io/valtlai/pen/qBwYezG?editors=1010

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior

React does not recognize some character references but renders them as is.

## The expected behavior

React should recognize all the specced character references that end with a semicolon and render the characters they represent.
