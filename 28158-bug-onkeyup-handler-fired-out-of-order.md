# Bug: onKeyUp Handler fired out of order

> Issue #28158 - Created on 1/30/2024

> Original URL: https://github.com/facebook/react/issues/28158

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
Initially found in version `18.2.0`

## Steps To Reproduce

1. Set up a react environment and create a simple DOM with one input element.
2. Add a reference and a state
```javascript
const textRef = useRef("");
const [typedText, setTypedText] = useState("");
```
3. Set up a div to display `typedText` on your website.
4. Add a KeyUp Event Listener to the input element:
```javascript
<input onBlur={() => setFocused(false)} onFocus={() => setFocused(true)} onKeyUp={(event) => {
        if (event.key.length === 1) {
          console.log(event.key)
          textRef.current += event.key;
          setTypedText(textRef.current);
        }
})>
```
5. Focus the input element, start typing a text with more than 80 WPM


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
https://codesandbox.io/p/sandbox/nervous-surf-vk68ck

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

<img width="538" alt="image" src="https://github.com/facebook/react/assets/72965843/e3b421c6-d99c-440d-bf1d-c633d557b0f1">

The first letter S is not upper case, the letters e, l in example were confused.
Platform: `Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:123.0) Gecko/20100101 Firefox/123.0`

## The current behavior
The order is not correct. The shift key often does not work for the first letter immediately afterwards when typing quickly.
It is very likely that the same result occurs again after reloading the page. React seems to be prone to only get certain combinations wrong.

## The expected behavior
```textRef.current == content of input element```
