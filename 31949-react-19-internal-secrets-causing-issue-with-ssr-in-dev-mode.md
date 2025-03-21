# [React 19] Internal secrets causing issue with SSR in dev mode

> Issue #31949 - Created on 1/1/2025

> Original URL: https://github.com/facebook/react/issues/31949

## Description

In React 19, the internal secret variable was renamed to `_DO_NOT_USE_OR_WARN_USERS_THEY_CANNOT_UPGRADE`. 
My first question is, why does it need to be prefixed with `__CLIENT_INTERNALS` and `__SERVER_INTERNALS`? 
This causes an issue with my precompiled component library. I don't give those components `"use client"` directive because it's an icon library that doesn't need any hook. So, NextJS rendered them on server and this happened
![image](https://github.com/user-attachments/assets/07ca17b1-0d38-4442-b319-78bf4265cc10)

I inspected the code of my icon library and found this
```js
import y3 from "react";
...
/**
 * @license React
 * react-jsx-runtime.development.js
 *
 * Copyright (c) Meta Platforms, Inc. and affiliates.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */
...
    function O() {
      var e = v.A;
      return e === null ? null : e.getOwner();
    }
...
    var f3 = y3, ... v = f3.__CLIENT_INTERNALS_DO_NOT_USE_OR_WARN_USERS_THEY_CANNOT_UPGRADE, ...
...
```

I noticed the internal secret is named `__SERVER_INTERNALS_DO_NOT_USE_OR_WARN_USERS_THEY_CANNOT_UPGRADE` on server.
![server internals](https://github.com/user-attachments/assets/27a28cad-e35d-4a6a-b5f6-a03c5a6d1f20)

The error was solved when I manually changed the code.
```js
...
    var f3 = y3, ... v = f3.__SERVER_INTERNALS_DO_NOT_USE_OR_WARN_USERS_THEY_CANNOT_UPGRADE, ...
...
```

My last question, is there any way to make the compiled code to use server secret if the client secret is not available and vice-versa? I don't want to manually edit the code after compiling them whenever I add new icons in future

Thank you!

PS. The error only happens when I run `npm run dev`.
