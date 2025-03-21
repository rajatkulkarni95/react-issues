# Bug:  Cannot read properties of null (reading 'useState')

> Issue #27987 - Created on 1/18/2024

> Original URL: https://github.com/facebook/react/issues/27987

## Description

Cannot read properties of null (reading 'useState')
TypeError: Cannot read properties of null (reading 'useState')
    at useState (http://localhost:3000/static/js/bundle.js:75196:25)
    at Q (http://localhost:3000/static/js/bundle.js:82555:61)
    at renderWithHooks (http://localhost:3000/static/js/bundle.js:24955:22)
    at mountIndeterminateComponent (http://localhost:3000/static/js/bundle.js:28239:17)
    at beginWork (http://localhost:3000/static/js/bundle.js:29535:20)
    at HTMLUnknownElement.callCallback (http://localhost:3000/static/js/bundle.js:14551:18)
    at Object.invokeGuardedCallbackDev (http://localhost:3000/static/js/bundle.js:14595:20)
    at invokeGuardedCallback (http://localhost:3000/static/js/bundle.js:14652:35)
    at beginWork$1 (http://localhost:3000/static/js/bundle.js:34516:11)
    at performUnitOfWork (http://localhost:3000/static/js/bundle.js:33764:16)
    
    How to solve this issue???
