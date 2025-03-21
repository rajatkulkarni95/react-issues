# [React 19] is the new compiler remove this unnecessary usgae of the useCallback

> Issue #31924 - Created on 12/27/2024

> Original URL: https://github.com/facebook/react/issues/31924

## Description

Hello,
using React 19 with the implementation of the new compiler (babel-plugin-react-compiler), no need to use useCallback and memo... explicitly because the new compiler do this job (as react compiler documentation).
my question is if explicitly i use useCallback with a function in my functional component not need the usage of useCallback (significant performance gains). is the new compiler remove this unnecessary usage of the useCallback?

thanks...
