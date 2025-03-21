# Bug: Definition for rule 'react-hooks/exhaustive-deps' was not found

> Issue #31458 - Created on 11/8/2024

> Original URL: https://github.com/facebook/react/issues/31458

## Description

Hi! 
I just migrated to the new eslint flat config file and I am getting the following error when I want to omit the
 `react-hooks/exhaustived-deps` rule:
 
![image](https://github.com/user-attachments/assets/20930ec2-ecff-4ac5-8727-02c1607f1158)


React version: "^18.3.1"

## Steps To Reproduce
I created a reproduction environment starting from the `vite-react` template provided by stackblitz and convertit to webpack. 
❗When using vite, this error doesn't appear. 
If you remove the comment `// eslint-disable-line react-hooks/exhaustive-deps` and run `npm run lint` you will get in the terminal the warning provided by eslint to add a dependency to the useLayoutEffect array. 
When I have the comment, the `npm run lint` run wihtout warnings or errors.
https://stackblitz.com/edit/vitejs-vite-egb7ki?file=src%2FApp.jsx

## The current behavior
Definition for rule 'react-hooks/exhaustive-deps' was not found

## The expected behavior
To be able to omit 'react-hooks/exhaustive-deps' when I need to.

Thanks!
