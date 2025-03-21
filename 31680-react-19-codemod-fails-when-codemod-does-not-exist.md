# [React 19] codemod fails when ~/.codemod does not exist

> Issue #31680 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31680

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

When running `npx codemod@latest react/19/migration-recipe` I get an error like...

```
Error: ENOENT: no such file or directory, scandir '/home/xxxx/.codemod'
    at async readdir (node:internal/fs/promises:948:18)
    at async Object.findCredentials (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:32395:12105)
    at async CYn (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:32395:12501)
    at async DYn.get (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:32405:302)
    at async Mne (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:32405:1787)
    at async QCi (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:52988:1393)
    at async R2e (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:52990:377)
    at async Object.handler (/home/xxxx/.npm/_npx/bef22f83919465d9/node_modules/codemod/dist/index.cjs:52990:1075) {
  errno: -2,
  code: 'ENOENT',
  syscall: 'scandir',
  path: '/home/xxxx/.codemod'
}
```

If I run `mkdir ~/.codemod` and then run the command again, it works normally.
