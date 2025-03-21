# [Code Refactor] Replace object checks with isObject function

> Issue #29020 - Created on 5/8/2024

> Original URL: https://github.com/facebook/react/issues/29020

## Description

I find there were many code place use 'type of xxx === 'object' && xxx !== null'
I think should use a util function named `isObject` to optimize this behavior.
I could add this function to shared and replace the before code.
should i do that? 


Looking forward to your feedback!
