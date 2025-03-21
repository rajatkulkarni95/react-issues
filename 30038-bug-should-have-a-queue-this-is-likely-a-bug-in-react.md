# Bug: "Should have a queue. This is likely a bug in React"

> Issue #30038 - Created on 6/22/2024

> Original URL: https://github.com/facebook/react/issues/30038

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

**React version:** 18.2.0 

(18.2.0 is required by Expo, but theoretically equivalent to 18.3.1 for this purpose)

## Steps To Reproduce

1. Unknown. No rules of hooks are being broken and the error stack is not helpful for diagnosis.

**Code example:**

I don't know how to reproduce this. Originally I faced #22049, supposedly caused by our "problem hook":

```js
// Supposed problem hook
const linkableRef = useRef(linkable);
useEffect(() => {
  linkableRef.current = linkable; // linkable is an array of objects
  const { current: editor } = editorRef;
  if (editor) editor.commands.updateLinkable();
}, [linkable, editorRef]);
```

and removing the hook causes this instead: `Error: Should have a queue. This is likely a bug in React. Please file an issue.`

## The current behavior
Using our simple hook causes #22049 - and removing our hook causes this issue instead

## The expected behavior
Using React as specified in the docs causes no errors
