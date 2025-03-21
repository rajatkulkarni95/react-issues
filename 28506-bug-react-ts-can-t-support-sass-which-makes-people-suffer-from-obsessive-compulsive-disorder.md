# Bug:  React-ts can't support sass, which makes people suffer from obsessive-compulsive disorder!

> Issue #28506 - Created on 3/6/2024

> Original URL: https://github.com/facebook/react/issues/28506

## Description

npx create-react-app  react-ts --template typescript

React version: 18.2.0

## Steps To Reproduce

1.  npx create-react-app  react-ts --template typescript
2.  When you create the simplest component using Sass, you find that it doesn't work properly!  This is just a small problem, but it's pretty maddening! ! ! Or you can just remove the default support for sass! ! !


error:
Cannot find module './index.scss' or its corresponding type declarations.
    1 | import React, { useEffect } from 'react';
  > 2 | import styles from './index.scss';

Shanghai China


