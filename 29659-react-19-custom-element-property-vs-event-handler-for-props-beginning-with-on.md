# [React 19] custom element property vs. event handler for props beginning with "on"

> Issue #29659 - Created on 5/30/2024

> Original URL: https://github.com/facebook/react/issues/29659

## Description

## Summary

Per discussion in issue #11347 and in PR #22184, the current implementation of custom element support in React 19 does the following:

1. checks if the react prop name begins with `on`
2. checks if the react prop value is of type `function`

If both conditions hold, it will `addEventListener` for an event based off of the remaining name, also using naming conventions to check if the suffix is `Capture` to determine whether or not to use capture phase for the event.

**Example:**
```jsx
<my-custom-element
  // This will listen for events of type `"customevent"`
  oncustomevent={(evt) => console.log(evt.type)}
  // This will listen for events of type `"customevent"` and will `useCapture`(See: https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#usecapture)
  oncustomeventCapture={(evt) => console.log(event.eventPhase, event.type)}
/>
```

In the aforementioned discussions, there was some debate on how to approach events, namely:

> I originally proposed that we do the same thing as preact here (forward everything starting with "on" to addEventListener), but if I remember correctly Sebastian felt strongly that we shouldn't reserve everything starting with "on" for event listeners. Jason Miller also felt strongly about this the other way, so maybe it's something that I can revisit/discuss more after merging this PR - maybe more users will chime in if they get to test it out.
- https://github.com/facebook/react/pull/22184#issuecomment-987510813 from @josepharhar 

Referencing this, @jfbrennan called out, among other things, the relevant bits of the [HTML Standard](https://html.spec.whatwg.org/dev/webappapis.html#event-handler-attributes)
(See: https://github.com/facebook/react/issues/11347#issuecomment-1767301646)

I **believe** there is a simple path forward to strike a balance here while still having support that is "idiomatically React"

## Proposal

Prefer the "in heuristic" even for properties that meet the two conditions mentioned above over adding an event listener.

### Motivation

- For cases that conform to the HTML standard for custom element properties/IDL attributes, a property intended to handle events should behave the same as the current implementation: namely, if I (or react-dom) set `myCustomElement.oncustomevent = (evt) => console.log(evt.type);`, this should add an event listener "under the hood"
- For cases where custom element authors have built properties that _**happen**_ to begin with `"on"` and _**happen**_ to accept functions as values, these will still work as expected, e.g. if there is a property on `my-custom-element` named `"onto"` it will get set as expected, even if the value is a function, so, e.g.
```jsx
<my-custom-element
  // This will be set as the value of property `"onto"`, even though it begins with `"on"` and its value is of type `function`
  onto={(value) => console.log(value)}
/>
```
### Current workarounds

- Use hooks (e.g. `useRef()` + `useEffect()`, etc.) to set these properties
- Expect web component authors to have a 2nd property whose name **_does not_** begin with `"on"` that mirrors the functionality of the property whose name _**does**_ begin with `"on"`.

### Relevant code

https://github.com/facebook/react/blob/main/packages/react-dom-bindings/src/client/DOMPropertyOperations.js#L194-L222

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

cc @jakearchibald @rickhanlonii for visibility
