# Issue while migrating from 18.2.0 to 19.0.0

> Issue #32084 - Created on 1/16/2025

> Original URL: https://github.com/facebook/react/issues/32084

## Description



I am migrating React 18.2.0 to 19.0.0. I first updated it to 18.3.1 as it was recommended and faced no issues on UI so far. 
I updated all the required dependencies and installed react and react-dom 19.0.0.

but when I am trying to proceed next with migration recipe. I am facing below error.
My proxies are properly set as I am able to install all the other packages from NPM.

``$ npx codemod@latest react/19/migration-recipe
✖ Fetching "react/19/migration-recipe"...

Error while fetching codemod react/19/migration-recipe: AxiosError: Request failed with status code 407``

How can I fix this ?

