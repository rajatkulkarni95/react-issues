# Suggestion for improve the code splitting mechanism

> Issue #29059 - Created on 5/15/2024

> Original URL: https://github.com/facebook/react/issues/29059

## Description

Hi, everyone)
The diagram illustrates the architecture and request flow:
![ARCH  BFF with Secure SPA Part](https://github.com/facebook/react/assets/96373865/850b2c3e-b5d8-40dd-b31a-29e7cb0922a2)
We need a simple way to separate the JS bundle of the solution into different folders. This way, in the BFF, we can check the requested part of the FE by root: if the request is for the content of a folder, for example, '/secure/..', then we can verify at the BFF level whether the user is authenticated.
This is necessary so that we do not return the entire SPA with potentially sensitive information for unauthenticated users.
Do you plan to enhance the code splitting mechanism to specify the folder where js chunks should be placed?) Do you have any recommendations?)


