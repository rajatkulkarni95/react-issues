# Bug: react version and @react/types version are incompatible

> Issue #29040 - Created on 5/10/2024

> Original URL: https://github.com/facebook/react/issues/29040

## Description

React and @types/react are installed in the project, but the versions do not match. useReducer error in Eslint.

React version:  18.2.0
when I install @types/react  with version: 18.2.69, but actual version 16.8.0 in project.

<img width="346" alt="image" src="https://github.com/facebook/react/assets/160737733/c7e83939-0023-4da7-b4b3-6de02055c5be">


## Steps To Reproduce

1. `import { useReducer } from 'react'` 
2. 
<img width="638" alt="image" src="https://github.com/facebook/react/assets/160737733/c8c638a2-0098-4e00-a365-42edcdd26e8c">

3. The third parameter of useReducer is required, which does not match the intended use case of the API. 



