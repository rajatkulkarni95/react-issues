# Bug: useRef on react-test-renderer wont work

> Issue #27775 - Created on 12/2/2023

> Original URL: https://github.com/facebook/react/issues/27775

## Description

Already trie jest.spyOn but no locl
Also why does the example on the page doesnt include how to test component with useRef?

```js
// Tooltip.test.js
import React from 'react'

import Tooltip from './Tooltip'
const renderer = require('react-test-renderer')
afterEach(() => {
  jest.clearAllMocks();
});
afterAll(() => {
  jest.resetAllMocks();
});


test('shows the children when the checkbox is checked', () => {
  const testMessage = 'Test Message'
  let root;
  renderer.act(() => {
    root = renderer.create(<Tooltip id="testing" message={"Test message property"}>{testMessage}</Tooltip>)
  });
})

```


```js
// Tooltip.js

import PropTypes from 'prop-types'
import { useEffect, useMemo, useRef } from 'react'


const Tooltip = ({
  id = 'tooltip',
  message,
  children
}) => {
  const el = useRef(null)
  const containerId = useMemo(() => {
    return 'tooltip-' + id
  }, [id])
  useEffect(() => {
    setTimeout(() => {
      try {
        new HSTooltip(el.current)
      } catch (e) {
        console.log(e)
      }
    }, 300)
  }, [])
  return (
    <div className="hs-tooltip inline-block">
      <div className='hs-tooltip-toggle'>
        {children}
      </div>
      <span ref={el} id={containerId} className="hs-tooltip-content hs-tooltip-shown:opacity-100 hs-tooltip-shown:visible opacity-0 transition-opacity inline-block absolute invisible z-10 py-1 px-2 bg-gray-900 text-xs font-medium text-white rounded shadow-sm dark:bg-slate-700" role="tooltip">
        {message}
      </span>
    </div>
  )
}
Tooltip.propTypes = {
  id: PropTypes.string,
  message: PropTypes.oneOfType([PropTypes.string, PropTypes.element]),
  children: PropTypes.oneOfType([PropTypes.string, PropTypes.element])
}

export default Tooltip
```
