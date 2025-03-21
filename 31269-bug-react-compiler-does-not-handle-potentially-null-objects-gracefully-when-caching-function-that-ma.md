# Bug: React-compiler does not handle potentially null objects gracefully when caching function that may not be run due to short-circuit evaluation

> Issue #31269 - Created on 10/16/2024

> Original URL: https://github.com/facebook/react/issues/31269

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: React 18; 
react-compiler-runtime: 0.0.0-experimental-605e95c-20241015
babel-plugin-react-compiler: 0.0.0-experimental-605e95c-20241015

## Steps To Reproduce

1. Use the current react-compiler-runtime / babel-plugin-react-compiler with the small repro shown in this link

[React compiler playground link](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdOuPz4A9NPwBRGDBxgANPjBMGCfEwK4YTBGHy4I+MnERgTAAz0IAtgDpHxsGQDmCW7rY5iGFNzOEsACx09fAB3CLYHR10TOipKZ3wAFTCmEzAw6EpCfFoGZlZTCI0yNwsTMnjHN0ImMlwESk4AWi0ANwgAawRCTpLGFjp1ACMoAkIIY3w6CFxnSXwYBFxYNgAeAGV8vDgmeCg9ACUEOkCNfKpCS+uEGABeYHJKMAQAX3x+rUIbxSlEovwSQNSv2kAD5xN9xOJRmU2AccLhjqcLldAvwxGxbgUHtjnqo1v9rqT8QlKd9hHipEjxutiTAAJJtRxCERrKRgaJ6OBhfD8cmEOk8qT4UJffCiEBuGxeBBy5ASyXMrYwXbNHrQ4AJVzuJXfHbSHXQgDcaqIpAo1FV+PVUg2mrYwMoVsd+Hh+J9zs223wO3NwDyhMeNwAZJHmU82RyhCazUxdZ7viBvkA)


## The current behavior
Errors when trying to access `null` object

## The expected behavior
Should not access `null` object which would not be accessed without compiler due to short-circuit evaluation.
