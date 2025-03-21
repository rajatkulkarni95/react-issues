# Bug: Spurious warnings in react dev runtime about using "key" property in spread object

> Issue #28943 - Created on 4/28/2024

> Original URL: https://github.com/facebook/react/issues/28943

## Description

This warning: https://github.com/facebook/react/blame/190cc990e01e5131a6b26f1a3212444cebd794e2/packages/react/src/jsx/ReactJSXElement.js#L530

Is triggering any time a rest-spread operator passes a key in an array.

That means even intentional and valid situations like:

```javascript
import {createRoot} from 'react-dom/client';

const component_props = [{
  key: 'my id',
  style: {
    color: 'red'
  },
  children: 'test'
}, {
  key: 'my second id',
  style: {
    color: 'green'
  },
  children: 'test2'
}];

const ComponentArray = props => component_props.map(p => <div {...p}/>);

const root = document.getElementById('root');
const vdom = createRoot(root);

vdom.render(<ComponentArray/>);
```

Are generating a heap of warnings when running in dev mode.

I understand the intention to try to avoid unintentional overwriting of a separate supplied key, but is the intention honestly to say you can no longer supply keys externally whatsoever?

React version: 18.2.0

## Steps To Reproduce

Run the sample above.

## The current behavior

Generates the following warning in development mode:

```
react_jsx-dev-runtime.js:92 Warning: A props object containing a "key" prop is being spread into JSX:
  let props = {key: someKey, style: ..., children: ...};
  <div {...props} />
React keys must be passed directly to JSX without using spread:
  let props = {style: ..., children: ...};
  <div key={someKey} {...props} />
    at ComponentArray
```

## The expected behavior

No warning should be generated - there is no other JSX key property being passed that might cause a collision here.
