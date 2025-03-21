# Bug: React Compiler should not encode in JSX prop value

> Issue #29120 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29120

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 19.0.0-beta-26f2496093-20240514

## Steps To Reproduce

Link to code example:

**Input Code**

```jsx
'use client';

function Comp() {
  return (
    <div aria-label="我能吞下玻璃而不伤身体">
      我能吞下玻璃而不伤身体
    </div>
  )
}
```

**React Compiler Output**

```jsx
function Comp() {
  const $ = _c(1);

  let t0;

  if ($[0] === Symbol.for("react.memo_cache_sentinel")) {
    t0 = (
      <div aria-label="\u6211\u80FD\u541E\u4E0B\u73BB\u7483\u800C\u4E0D\u4F24\u8EAB\u4F53">
        我能吞下玻璃而不伤身体
      </div>
    );
    $[0] = t0;
  } else {
    t0 = $[0];
  }

  return t0;
}
```

[React Compiler Playground](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAcimBACOAbASwQDsAXNAbgB1iaAzKYuUgiY7AYQgFsAHACgCU2YDWzYYCUrHb8x47AB4AJgQBu2AIYwCmgLR5NAIwR4AvFRCBEI0C-AYDwVQNBygbudAwS6AYAMCwcoBJ5QNVxgZXlLAD55BWxbR1dPXwD2BUUAelU1YNjBGgBfGhB0oA)

**Babel / SWC / ESBuild JSX transform**

SWC:

```jsx
"use client";
import { jsx as _jsx } from "react/jsx-runtime";
function Comp() {
    var $ = _c(1);
    var t0;
    if ($[0] === Symbol.for("react.memo_cache_sentinel")) {
        t0 = _jsx("div", {
            "aria-label": "\\u6211\\u80FD\\u541E\\u4E0B\\u73BB\\u7483\\u800C\\u4E0D\\u4F24\\u8EAB\\u4F53",
            children: "我能吞下玻璃而不伤身体"
        });
        $[0] = t0;
    } else {
        t0 = $[0];
    }
    return t0;
}
```

[SWC Playground](https://play.swc.rs/?version=1.3.100&code=H4sIAAAAAAAAA01QzUrEMBi89yk%2BysK2B9d229UFrWDX7gt4tFK6McVAmkibCCILwl4Ef%2FDn7smbL7Co%2BzbV7WOYpApekuGbyWTm68saA6IEM9HfsaxCMiQIZzDh5ZnjwqUFgDirBfQgggw5vqtUABQLEJ6BpACnd%2BQdQxRFcHhRzjgdFLxy7ArnSAxKXPIM5egUZ7X6hDBMbbczBmWhXB0DAXZPyDnkFck3aD7DNLJTuTX0%2FVSOvelBKkehn6QyTLw4ldtBrM9wHGjWm5i50oTTYagmyX6s8Siw9369Ab6vH9vF6uvhpVnerO8%2F1k%2BL9uq2Wd41n6%2Ft%2B1uzev5LsalidM9UVX115UxdgDlgqjb2L76mDaOXUWEhK2a0c%2BsHdwVYe1wBAAA%3D&config=H4sIAAAAAAAAA12QMW7DMAxF95zC4Jy1HTp2y9BDEAodsDAlgaSAGoHvHsmxHKeb%2BN8nP8X7aRjg1wJ8Dff6rEVGNdK9rorN0fGvKuBzJgvK2eHcqVtDroV26TpHFA4XyUl9gytbnhZw1Bs1AmQf0EXFaGNSOWYrYfCDUKVi9F14co72L7j5S3QWaqOxeBJ0DrDh5W0H4cjjfMwKSbKStakjTvb6j2C8TdTltylTSkbHhhUA20%2B6lrWnL%2FgK3L0g3bTdvt33eZXPtvRyWh5kw2%2F9oAEAAA%3D%3D)

Babel:

```jsx
"use strict";
'use client';

var _jsxRuntime = require("react/jsx-runtime");
function Comp() {
  const $ = _c(1);
  let t0;
  if ($[0] === Symbol.for("react.memo_cache_sentinel")) {
    t0 = /*#__PURE__*/(0, _jsxRuntime.jsx)("div", {
      "aria-label": "\\u6211\\u80FD\\u541E\\u4E0B\\u73BB\\u7483\\u800C\\u4E0D\\u4F24\\u8EAB\\u4F53",
      children: "\u6211\u80FD\u541E\u4E0B\u73BB\u7483\u800C\u4E0D\u4F24\u8EAB\u4F53"
    });
    $[0] = t0;
  } else {
    t0 = $[0];
  }
  return t0;
}
```

[Babel REPL](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=OQVwzgpgBAxgNgSwgOwC7ANwCgsDMTIyoID2yUAwiQLYAOAFAJRQDeWUsZYqUAJFAF4oAfRj0AjI2zsocCD1QAGaRwS4o9XgG1FAXUEChAZQCe1AEYk4AOlwkATvQBE9iAEMi16hGolRHgAsIYUg0BGQIOCdGZjYODiVBDRl4qAAeABMEADcoN3sENwBaODdzSIEnAB0QADYAJnFxGoAORQAxABEagFYAFnEAURq-wcUAIRqAdgBmccmQKb6WmdbFRQoRse6QPvb6vtbBgEEFvZ6ZpwA-FNSoQEQjQF-AwDwVQGg5QG7nQGCXQBgAwFg5QBJ5QDVcYBleVuHDSAHostkbqkpLdtHokkpsBwAL5QSKQVi3RJCRG6VFQNE4DiuVAgezkFFYElAA&debug=false&forceAllTransforms=false&modules=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2&prettier=false&targets=&version=7.24.5&externalPlugins=%40babel%2Fplugin-transform-modules-commonjs%407.23.0&assumptions=%7B%7D)

ESBuild:

```jsx
'use client'

import { jsx } from "react/jsx-runtime";
function Comp() {
  const $ = _c(1);
  let t0;
  if ($[0] === Symbol.for("react.memo_cache_sentinel")) {
    t0 = /* @__PURE__ */ jsx("div", { "aria-label": "\\u6211\\u80FD\\u541E\\u4E0B\\u73BB\\u7483\\u800C\\u4E0D\\u4F24\\u8EAB\\u4F53", children: "\u6211\u80FD\u541E\u4E0B\u73BB\u7483\u800C\u4E0D\u4F24\u8EAB\u4F53" });
    $[0] = t0;
  } else {
    t0 = $[0];
  }
  return t0;
}
```

[ESBuild REPL](https://hyrious.me/esbuild-repl/?version=0.21.3&t=function+Comp%28%29+%7B%0A++const+%24+%3D+_c%281%29%3B%0A%0A++let+t0%3B%0A%0A++if+%28%24%5B0%5D+%3D%3D%3D+Symbol.for%28%22react.memo_cache_sentinel%22%29%29+%7B%0A++++t0+%3D+%28%0A++++++%3Cdiv+aria-label%3D%22%5Cu6211%5Cu80FD%5Cu541E%5Cu4E0B%5Cu73BB%5Cu7483%5Cu800C%5Cu4E0D%5Cu4F24%5Cu8EAB%5Cu4F53%22%3E%0A++++++++%E6%88%91%E8%83%BD%E5%90%9E%E4%B8%8B%E7%8E%BB%E7%92%83%E8%80%8C%E4%B8%8D%E4%BC%A4%E8%BA%AB%E4%BD%93%0A++++++%3C%2Fdiv%3E%0A++++%29%3B%0A++++%24%5B0%5D+%3D+t0%3B%0A++%7D+else+%7B%0A++++t0+%3D+%24%5B0%5D%3B%0A++%7D%0A%0A++return+t0%3B%0A%7D&o=--jsx%3Dautomatic+--loader%3Djsx)

## The current behavior

The prop value becomes double escaped.

## The expected behavior

The prop value should only be escaped once.

