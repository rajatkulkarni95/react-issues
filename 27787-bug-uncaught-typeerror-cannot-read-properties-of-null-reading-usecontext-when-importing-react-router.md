# Bug:  Uncaught TypeError: Cannot read properties of null (reading 'useContext') when importing react-router-dom

> Issue #27787 - Created on 12/4/2023

> Original URL: https://github.com/facebook/react/issues/27787

## Description

<!--
  I have created several react apps and whenever I go to import the react-router-dom by installing using 'npm i react-router-dom', I receive this error 'Uncaught TypeError: Cannot read properties of null (reading 'useContext')' and this one 'Uncaught (in promise) Error: A listener indicated an asynchronous response by returning true, but the message channel closed before a response was received'. I have tried several solutions listed online to no avail. I am not breaking the rules of hooks and I do not have multiple or mismatched versions of React. 
-->

React version:

## Steps To Reproduce

1. Create a basic React app by using npx create-react-app name of app
2. import Link or BrowserRouter from 'react-router-dom' and you will get the error and a blank screen. 


![image](https://github.com/facebook/react/assets/120531347/92c566a3-b981-457d-924e-6af7b0b7db9f)


## The current behavior
Giving me an error in the console.

## The expected behavior
Use react-router-dom and have the code appear in the browser.
