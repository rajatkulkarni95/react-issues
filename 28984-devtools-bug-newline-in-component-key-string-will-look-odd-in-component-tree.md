# [DevTools Bug]: Newline in component key string will look odd in component tree

> Issue #28984 - Created on 5/3/2024

> Original URL: https://github.com/facebook/react/issues/28984

## Description

### Website or app

/

### Repro steps

Create an element with a key like `Foo\n\n\n\nBar\n\n\n\nBaz` and it will occupy multiple lines in the component tab.

```
<div className='App'>
  <h1 key="0-hello\nworld\nfoo\nbar\nbaz">Hello React.</h1>
  <h1 key="1-hello\nworld\nfoo\nbar\nbaz">Hello React.</h1>
</div>
```

Here's a screenshot:

<img width="658" alt="react-devtools-bug" src="https://github.com/facebook/react/assets/72194488/5fed3830-e4dd-48f7-ab73-b0e30ed70b44">


Background: I've worked on a syntax-highlighter which adds a <span> for each section of text that's colored differently.
As key, I use the index of the element, it's format name and the actual content of the element.
The content can contain whitespaces or blank lines. It can also be very long strings.

### How often does this bug happen?

Every time

### DevTools package (automated)

_No response_

### DevTools version (automated)

_No response_

### Error message (automated)

_No response_

### Error call stack (automated)

_No response_

### Error component stack (automated)

_No response_

### GitHub query string (automated)

_No response_
