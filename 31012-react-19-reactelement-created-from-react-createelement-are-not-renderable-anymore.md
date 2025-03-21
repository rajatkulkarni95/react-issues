# [React 19] - `ReactElement` created from `React.createElement` are not renderable anymore

> Issue #31012 - Created on 9/20/2024

> Original URL: https://github.com/facebook/react/issues/31012

## Description

## Summary

**TL; DR**

Using `React.createElement` in the `JSON.parse`'s revive function to deserialize json into `ReactElement`, but the returned value can no longer be rendered with errors:

```
Error: Objects are not valid as a React child (found: object with keys {key, props, _owner, _store}). If you meant to render a collection of children, use an array instead.
```

----

I am maintaining a docs site powered by React & Next.js **Pages Router**.

The docs site copy-pastes a risk approach of rendering MDX on the server serializing MDX components on the server and deserializing on the client from the React docs site:

https://github.com/reactjs/react.dev/blob/39abc60fce1588b4e83cc45d52b522aa63c01bc2/src/utils/compileMDX.ts#L145C1-L160C4
https://github.com/reactjs/react.dev/blob/39abc60fce1588b4e83cc45d52b522aa63c01bc2/src/pages/%5B%5B...markdownPath%5D%5D.js#L104-L128


I have slightly modified the `reviveNodeOnClient` function to use `React.createElement` instead:

```diff
function reviveNodeOnClient(key: unknown, val: unknown) {
  if (Array.isArray(val) && val[0] === '$r') {
    // Assume it's a React element.
    let type = val[1];
    const key = val[2];
    let props = val[3];
    if (type === 'wrapper') {
      type = Fragment;
      props = { children: props.children };
    }
    if (type in MDXComponents) {
      type = MDXComponents[type];
    }
    if (!type) {
      if (process.env.NODE_ENV !== 'production') {
        // eslint-disable-next-line no-console -- log error
        console.warn(`Unknown type: ${type}`);
      }
      type = Fragment;
    }
-    return {
-      $$typeof: Symbol.for('react.element'),
-      type: type,
-      key: key,
-      ref: null,
-      props: props,
-      _owner: null,
-    };
+    return createElement(type, key ? Object.assign(props, { key }) : props);
  }
  return val;
}
```

Yet, I get this error:

```
Error: Objects are not valid as a React child (found: object with keys {key, props, _owner, _store}). If you meant to render a collection of children, use an array instead.
```

## Reproduction

Repo `SukkaW/mirrorz-help` with branch `housekeeping`.

https://github.com/SukkaW/mirrorz-help/tree/housekeeping


