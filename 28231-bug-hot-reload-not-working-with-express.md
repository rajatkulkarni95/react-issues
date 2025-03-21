# Bug: hot-reload not working with express

> Issue #28231 - Created on 2/4/2024

> Original URL: https://github.com/facebook/react/issues/28231

## Description

Hello everyone, has anyone ever had hot reload stop working? since yesterday it doesn't work in react when I'm connected to express. When express is OFF it works, and in another project it works despite the connection to the server
in this project I have the main Home page and it does not respond to changes hot-reload, loads the build directory, every time I need to do an npm run build
[https://streamable.com/fbqho6](https://streamable.com/fbqho6?fbclid=IwAR1gL78My6pcrBg6wBfpY1BHcnKLENhvCV2Vcx8FnU4WHisdXaGQdbeSb7c)
and when I run another project with the server express, it works
[https://streamable.com/377x81](https://streamable.com/377x81?fbclid=IwAR3LWxTuFEu_zhuY-VUDZL4oqJeDB7onxRpXhdL7xBLoin-kBfqt7Zo1Lr0)
I think it happened after uninstalling websocket.io but I'm not sure, I looked for solutions in Google but none of them work, I made a clean project and copied the files, installed the dependencies and still the same
