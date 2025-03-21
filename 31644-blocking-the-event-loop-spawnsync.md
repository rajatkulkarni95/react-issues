# Blocking the event loop spawnSync 

> Issue #31644 - Created on 11/28/2024

> Original URL: https://github.com/facebook/react/issues/31644

## Description

To avoid blocking event loop use **execSync** is best compare to **SpawnSync** this cause performance, when running multiple concurrent tasks in  React build pipeline

**Consider replacing `spawnSync` with `spawn` to prevent blocking**

```js
const sha = execSync('git rev-parse HEAD').slice(0, 8);

