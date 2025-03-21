# I am very much looking forward to React having an ESM bundle version similar to Vue, specifically designed for the tree Shaking feature in Rollup, which is convenient to package into NginxScript's njs for SSR use

> Issue #28442 - Created on 2/26/2024

> Original URL: https://github.com/facebook/react/issues/28442

## Description

I am very much looking forward to React having an ESM bundle version similar to Vue,
This makes it more convenient to use the tree shading function specifically for scrolling,
Currently, it is convenient to package it into NginxScript njs for SSR use
Looking forward to providing a lightweight React dom/Server module version specifically designed for NginxScript for njs

>* 1.js
```js
import a from "./2.js"
console.log(a())
```
>* 2.js
```
import 'core-js/actual/map';
import 'core-js/actual/set';
import {createElement} from 'react';  
import { renderToString } from 'react-dom/server'; 

function App1(){
  return createElement("div",{},'ffgd',  createElement("a",{},'d'))
}
function App(){
  return createElement(App1)
}
  
export default () => {
  const context = {};  
  const appWithHelmet = createElement(App);  

  const html = renderToString(appWithHelmet);  
  // const helmet = Helmet.renderStatic();  
  return html;
}
```

>* rollup.config.js
```js
import commonjs from '@rollup/plugin-commonjs'
import babel from '@rollup/plugin-babel'
import resolve from '@rollup/plugin-node-resolve'
import polyfillNode from 'rollup-plugin-polyfill-node'

// List of njs built-in modules.
const njsExternals = ['crypto', 'fs', 'querystring']

/**
 * Plugin to fix syntax of the default export to be compatible with njs.
 * (https://github.com/rollup/rollup/pull/4182#issuecomment-1002241017)
 *
 * @return {import('rollup').OutputPlugin}
 */
const fixExportDefault = () => ({
  name: 'fix-export-default',
  renderChunk: (code) => ({
    code: code.replace(/\bexport { (\S+) as default };/, 'export default $1;'),
    map: null,
  }),
})
const fixTextEncoderDefault = () => ({
  name: 'fix-TextEncoder-default',
  renderChunk: (code) => ({
    code: code.replace(/\butil.TextEncoder/, 'TextEncoder'),
    map: null,
  }),
})
export default {
  input: 'src/1.js', // 主入口文件  
  output: {
    file: 'src/1.bundle.js', // 输出的打包文件  
    format: 'es' // 输出格式，这里使用 IIFE（立即调用函数表达式）  
  },

  external: njsExternals,
  plugins: [ /* 插件配置 */
    // Transpile TypeScript sources to JS.
    babel({
      babelHelpers: 'bundled',
      envName: 'njs',
      extensions: ['.ts', '.mjs', '.js'],
    }),
    polyfillNode(),
    // Resolve node modules.
    resolve({
      extensions: ['.mjs', '.js', '.json', '.ts'],
    }),
    // 将 CommonJS 模块 转换为 ES6 模块。
    commonjs(),
    // 针对NginxScript下的njs对默认导出语法的特色要求做修复，
    fixExportDefault(),
    // TextEncoder
    fixTextEncoderDefault(),
  ]
};
```
```json
{
  "name": "njs-app-test",
  "scripts": {
    "x":"rollup -c --bundleConfigAsCjs"
  },
  "devDependencies": {
    "@types/react":"^18.2.58",
    "core-js": "3.36.0",
    "rollup": "4.10.0",
    "rollup-plugin-esbuild": "6.1.1",
    "rollup-plugin-dts": "6.1.0",
    "@rollup/plugin-typescript": "11.1.6",
    "@rollup/plugin-commonjs": "25.0.7",
    "@rollup/plugin-babel": "6.0.4",
    "@rollup/plugin-node-resolve": "15.2.3",
    "rollup-plugin-polyfill-node": "0.13.0"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "peerDependencies": {
    "typescript": "~5"
  },
  "peerDependenciesMeta": {
    "typescript": {
      "optional": true
    }
  }
}
```
```shell
npm run x  && njs ./src/1.bundle.js
```
>* Demo preview
![image](https://github.com/facebook/react/assets/17898715/e0e58773-6575-4b86-be7f-06031864b876)
>* 1.bundle.js preview
![image](https://github.com/facebook/react/assets/17898715/bdd152e9-d9e1-4abe-9bcc-0ddfd1efe913)
```shell
njs -v
# 0.8.4
```

>* Based on the results of bundling a simple React rendering with Rollup, the file 26783 lines are too large. We hope to have a better optimization solution
