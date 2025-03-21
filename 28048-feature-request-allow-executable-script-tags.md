# Feature Request: Allow executable `script` tags

> Issue #28048 - Created on 1/22/2024

> Original URL: https://github.com/facebook/react/issues/28048

## Description

Currently, any `script` tag rendered with React is not executed because it is created as the `innerHTML` of a `div` element: (#5146). I recently was trying to figure out how to render a script tag with an `onLoad` callback through React and ran into this behavior. After looking through the source I realized this was a design decision, but I'm wondering if it would be possible to allow executable scripts, perhaps using a special `execScript={true}` prop to not break backwards compatibility.

After some experimentation, I was able to get this functionality working with a couple small modifications to `react-dom`, plus some minor changes for the `execScript` property to be recognized by React.

I'm curious if there is a good reason to disallow rendering executable `script` tags, as I looked through the commits to the code in question and didn't see much beyond it being a breaking change if it was enabled by default.

If this change is approved it would fix issue #13863 which I found early on into my search for the reasoning why my `onLoad` handler didn't work on a `script` tag.

The main changes to enable this functionality that I found are as follows:
- `react-dom-bindings/src/client/ReacDOMComponent.js:1279`: Add `case 'script':` to enable `load` and `error` events for script tags.
- `react-dom-bindings/src/client/ReactFiberConfigDOM.js:432`: Add a condition `if (props.execScript)` which will run `domElement = ownerDocument.createElement('script')` instead of the current `div` approach.
- `react-dom-bindings/src/shared/ReactDOMUnknownPropertyHook.js:189`: Add a `case 'execScript':` to the switch statement to treat `execScript` as a known reserved prop.
- `react-dom-bindings/src/shared/possibleStandardNames.js:63`: Add `execscript: 'execScript'` to the object to recognize the new prop key.

I'm opening this issue as I'm curious for the reasoning to disallow executable scripts and if it would be considered by the React team to allow this functionality in the future.

Currently there are workarounds involving running `const myScript = document.createElement('script'); ... document.appendElement(myScript);` in a `useEffect` which could be simplified by this proposal.

I'm open to any discussion on this topic. I haven't seen much about this in my research and am hoping something like this would be possible in the future. I don't fully understand the internals of React so I can't see what effect this would have for non `react-dom` renderers like `react-native`, but would love some input from somebody that does.

Additionally, NextJS has their own `next/script` component that has an `onLoad` handler to enable this in NextJS projects, which was where I first was experimenting with `<script onLoad={...}/>` before moving to other React frameworks/projects where I found this to be missing.
