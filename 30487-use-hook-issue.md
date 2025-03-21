# use hook issue 

> Issue #30487 - Created on 7/27/2024

> Original URL: https://github.com/facebook/react/issues/30487

## Description

react-dom_client.js?v=af78aa99:3617 Uncaught 
Error: async/await is not yet supported in Client Components, only Server Components. This error is often caused by accidentally adding `'use client'` to a module that was originally written for the server.
    at trackUsedThenable (react-dom_client.js?v=af78aa99:3617:23)
    at useThenable (react-dom_client.js?v=af78aa99:4742:20)
    at Object.use (react-dom_client.js?v=af78aa99:4749:57)
    at exports.use (chunk-WQZPVTOA.js?v=af78aa99:1049:36)
    at PostItems (Users.jsx:10:14)
    at react-stack-bottom-frame (react-dom_client.js?v=af78aa99:16336:20)
    at renderWithHooks (react-dom_client.js?v=af78aa99:4598:24)
    at updateFunctionComponent (react-dom_client.js?v=af78aa99:6175:21)
    at beginWork (react-dom_client.js?v=af78aa99:7222:20)
    at runWithFiberInDEV (react-dom_client.js?v=af78aa99:990:18)
![Screenshot 2024-07-26 222611](https://github.com/user-attachments/assets/f058f107-faa5-4cf2-accc-1b66e909e658)
![Screenshot 2024-07-26 222647](https://github.com/user-attachments/assets/668829a0-3b22-43a0-824f-94566e0284cd)

