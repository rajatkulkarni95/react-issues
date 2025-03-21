# Bug: mouse events are bubbled up too far with some pointer-events rules

> Issue #28817 - Created on 4/11/2024

> Original URL: https://github.com/facebook/react/issues/28817

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

If an element with the css rule `pointer-events: none` has a descendant with the rule `pointer-events: all`, then the descendant's mouse events are bubbled up to all of its ancestors

React version: 18.2

## Steps To Reproduce

1. 
```
import React from 'react'
import ReactDOM from 'react-dom'

function Container() {
  return (
    <div
      style={{padding: '20px', border: '1px solid #aaa', pointerEvents: 'none'}}
      onMouseLeave={(e) => console.log('container', e)}
      id="container"
    >
      <div onMouseLeave={() => {console.log('child 1')}}>
        <div
          style={{
            pointerEvents: 'none',
            border: '1px solid black',
            padding: '10px',
          }}
          onMouseLeave={() => {console.log('child with pointerEvents: none')}}
        >
          <div
            style={{
              width: '100px',
              height: '100px',
              backgroundColor: 'red',
              pointerEvents: 'all',
            }}
            onMouseLeave={() => {console.log('child with pointerEvents: all')}}
          />
        </div>
      </div>
    </div>
  )
}

function App() {
  return <Container />
}

ReactDOM.render(<App />, document.getElementById('root'))
```

2. Hover the rendered red square
3. Mouse away from it. Each component's `onMouseLeave` callback will be fired

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

https://codesandbox.io/p/sandbox/tender-smoke-cqk24y?file=%2Fsrc%2Findex.js%3A1%2C1-40%2C1

## The current behavior

The `onMouseLeave` event is propagated beyond the component which was actually left

## The expected behavior

The `onMouseLeave` trigger is called for the element which was moused away from, and not its parents
