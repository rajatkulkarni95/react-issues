# [React 19] react compiler warns about mutating ref in specific case

> Issue #29131 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29131

## Description

## Summary

im not sure what is the specific case here. i know that i dont get an error if i do any of the following:

- stop returning the `execute` func in the hook
- remove the useEffect
- remove the listener

![image](https://github.com/facebook/react/assets/18744505/daf7ae6f-d58e-483f-bfa1-5974e815d2c3)

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAHQHYDMobgFwEsIMACDCCAB1IAoBKU4TU0mBfWMjKAG18wBfTJhx4iJUlDAIAKgjD4GTFqTglFpAB6kAvFJkAlBFloVq9EWTUb8pBFoRwo+BHroBDAEYQY+AMIk+DAQ-AgwAPzIpACCPn6BGMGhvOGMugB8KtasrFoAdM4w7EkMqrk2GJrevvgAMoSKCBjh7sqZ2RUVNQlBIWGR+WCEAOYYHrz57AC2EABuCACiC0kNTS0wtADkPfhbADSku2uuG5Y5XQVFJXb65lTlucIXz6rSS1hYTkrtWcwX7E4MDIv20hVgNzK1kEhwA2gBdc6qQFcJj2RzOVykZ6vFpaKi1UgAExMHj4djEBGIZAAsgBPGJUKjKf6sFHA0gAHiJhDmGQAEgh+BBSAB1Xy8ImcgD0PL5AG4hJgQIIgA

