# Questions and Help: useMemo vs Normal Object

> Issue #27837 - Created on 12/15/2023

> Original URL: https://github.com/facebook/react/issues/27837

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: all

## Question

Which one these 2 below scenario is actually cheaper in terms of performance
1. using useMemo in a small object and giving dependency array and checking if something's changed in dependency array and act according to that.
2. don't use useMemo and believe that object creation on every render will be actually cheaper than using useMemo.


FYI - myStyle and myStyle2 is not being passed as props to some other component and the given component is a leaf component (present at the end of react tree)


<img width="534" alt="Screenshot 2023-12-15 at 9 27 05 AM" src="https://github.com/facebook/react/assets/102596512/1786b9ec-62a8-4123-95d2-64665bf09191">

