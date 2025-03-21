# [DevTools Bug] Could not find node with id "24823" in commit tree

> Issue #28107 - Created on 1/26/2024

> Original URL: https://github.com/facebook/react/issues/28107

## Description

### Website or app

react native app

### Repro steps

recoding profile

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-core

### DevTools version (automated)

4.28.0-9b95b131b

### Error message (automated)

Could not find node with id "24823" in commit tree

### Error call stack (automated)

```text
at C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1024248
    at Map.forEach (<anonymous>)
    at C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1024197
    at ar.getRankedChartData (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1024665)
    at Oc (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1236925)
    at en (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:40150)
    at Ci (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:58285)
    at Es (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:116447)
    at El (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:100131)
    at bl (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:100060)
```


### Error component stack (automated)

```text
at Oc (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1236682)
    at div
    at div
    at div
    at yo (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1145723)
    at C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1354530
    at hs (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1161269)
    at C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1163988
    at div
    at div
    at div
    at ms (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1163822)
    at rc (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1226474)
    at zu (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1218933)
    at lt (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1068120)
    at $t (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1095397)
    at Ts (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1167737)
    at r_ (C:\Users\khhus\AppData\Roaming\npm\node_modules\react-devtools\node_modules\react-devtools-core\dist\standalone.js:2:1361060)
```


### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Could not find node with id  in commit tree in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

