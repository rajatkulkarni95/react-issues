# parsePluginOptions lowercasing breaks runtimeModule option

> Issue #29110 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29110

## Description

The plugin options parser lowercases all option values : https://github.com/facebook/react/blob/94896cb8c5b1dfc80aa947ac9b273b6b9447571f/compiler/packages/babel-plugin-react-compiler/src/Entrypoint/Options.ts#L201

This breaks the `runtimeModule` option on case-sensitive filesystems (and the module path happens to contain uppercase characters). 
