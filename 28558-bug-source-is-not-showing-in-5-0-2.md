# Bug: Source is not showing in 5.0.2

> Issue #28558 - Created on 3/14/2024

> Original URL: https://github.com/facebook/react/issues/28558

## Description

## Stand 
DevTools version:  5.0.2-47cf347e4
Chrome 122.0.6261.129 x64, Edge 122.0.2365.80 x64

## Propblem
In the DevTools -> Components -> source. 
The path to the bundle.js file is specified.
#### v5.0.2
![image](https://github.com/facebook/react/assets/144036324/19ae23ca-0b5c-4e22-b2fb-20e69b8de53e)
![image](https://github.com/facebook/react/assets/144036324/5a31c30f-3729-40fa-a580-12546cd66945)
![image](https://github.com/facebook/react/assets/144036324/68806261-1588-4821-9787-e17aa2a10f0a)
![image](https://github.com/facebook/react/assets/144036324/cea28611-acfe-4e69-acbb-0cf8ff409af2)
#### v5.0.0
![image](https://github.com/facebook/react/assets/144036324/c363f00d-eedd-4f84-bc1d-dd6e027a55c4)
![image](https://github.com/facebook/react/assets/144036324/47b70158-5921-434c-8133-7f418dbb926c)
![image](https://github.com/facebook/react/assets/144036324/a69f6db7-59dd-4dc0-b316-16947924b5dd)
## Analog Issue
https://github.com/facebook/react/issues/28544
@hoxyq this is has nothing to do with reality.
But "source" **work** in "DevTools version: **5.0.0**-993c4d003"
And **doesnt wokr** in "DevTools version: **5.0.2**-47cf347e4"

Tested one application on the same PC at the same time in the defferent version DevTools.
Equal SourceMap

React version: 18

## The current behavior
Open DevTools, choose component -> the source field contains the name of the component

## The expected behavior
Open DevTools, choose component -> the source field says "bundle.js:[lineNumber]".


