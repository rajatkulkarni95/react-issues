# [React 19] Publishing the TypeScript declaration of `babel-plugin-react-compiler`

> Issue #29098 - Created on 5/16/2024

> Original URL: https://github.com/facebook/react/issues/29098

## Description

### Description

I am currently integrating React's new experimental compiler into my projects, specifically through the development of a Next.js plugin and a webpack loader, which can be found here: [react-compiler-webpack](https://github.com/SukkaW/react-compiler-webpack). During this process, I've encountered an issue where the TypeScript definitions for the new compiler are not available on npm. Since the compiler itself is written in TypeScript, having these definitions available would be immensely beneficial for ensuring type safety and enhancing developer productivity, especially in complex projects like Next.js and webpack plugins.

### Expected Behavior

The TypeScript definitions for React's new experimental compiler should be published to npm, allowing developers to import and use these definitions seamlessly in TypeScript-based projects.

### Current Behavior

The TypeScript definitions are not currently available on npm, which complicates the development process for TypeScript users who need to ensure type safety and utilize IDE features like auto-completion and inline documentation.

### Proposed Solution

I kindly request that the TypeScript definitions for the new experimental compiler be published to npm. This would not only aid in my current project but also benefit the broader TypeScript and React communities who are experimenting with or adopting the new compiler.

Thank you for considering this request. I am looking forward to any updates and am happy to assist in the testing or development of these definitions if needed.

