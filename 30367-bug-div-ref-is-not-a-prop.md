# Bug:  div: `ref` is not a prop

> Issue #30367 - Created on 7/18/2024

> Original URL: https://github.com/facebook/react/issues/30367

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

Using Vite & React we're getting the weirdest error i've seen in all my react career:
```
Warning: div: `ref` is not a prop. Trying to access it will result in `undefined` being returned. If you need to access the same value within the child component, you should pass it as a different prop. (https://reactjs.org/link/special-props)
```

I'm clueless, how does react warn me that `ref` is not a prop for `<div>`?

Accompanied is a whole bunch of other errors related to contexts:
```
Warning: _RichTextEditor: `key` is not a prop.
Warning: Rendering <Context.Consumer.Provider> is not supported and will be removed in a future major release. Did you mean to render <Context.Provider> instead?
Warning: Rendering <Context.Consumer.Consumer> is not supported and will be removed in a future major release. Did you mean to render <Context.Consumer> instead?
```

React version: `18.3.1`

## Steps To Reproduce

We tried to reproduce it but it does not happen in a minimal example.
Please advice on tactics/methods to write a minimal reproducible to try and get this error. 

The component giving this error is rendering a `createPortal` to the `document.body`:

![image](https://github.com/user-attachments/assets/89bae1ed-ea65-4baa-bc08-b03e88194d03)

Large Node Tree With recursively rendered components and form elements just to show it's a complex application which I think is what contributes to why we can't replicated it.

![image](https://github.com/user-attachments/assets/7dc300fa-33a9-4113-b598-5c7d1647fb29)


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: WIP

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
VM18671:1 Warning: div: `ref` is not a prop. Trying to access it will result in `undefined` being returned. If you need to access the same value within the child component, you should pass it as a different prop. (https://reactjs.org/link/special-props)

## The expected behavior
No Error
