# Bug: The solution for challenge 2 (Fix a retriggering animation) is an overkill. https://react.dev/learn/removing-effect-dependencies#challenges 

> Issue #27984 - Created on 1/18/2024

> Original URL: https://github.com/facebook/react/issues/27984

## Description

I think since the "show/remove" always destroy and recreate the "Welcome" component.  Simply remove the duration from useEffect dependency will solve the problem. 
