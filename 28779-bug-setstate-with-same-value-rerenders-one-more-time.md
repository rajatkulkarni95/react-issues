# Bug: SetState with same value, rerenders one more time

> Issue #28779 - Created on 4/8/2024

> Original URL: https://github.com/facebook/react/issues/28779

## Description

As far as I know, react's update machanism somehow checks the new value and current value of states to optimize rerenders. And I can see this behaviour after second time.

I tried 2 scenario. I put "console.log" just above return().

The first one is, I defined a state with initial value String "1". Then I tried to set the same value on button click. It never rerendered as expected.

The second scenerio is, I defined a state with initial value String "1". Then I tried to set another value String "2" on every button click. My expectation is it will rerender to set the value "2". But after setting the value "2" once, it should never rerender for value "2" if current value still "2". However it does one more time. After then, it wont rerender.  Is it expected behaviour ?

React version: 18.2.15

## Steps To Reproduce

1. By using my code sandbox below:
1.1. Enter the url
1.2 run the code
1.3 click the button twice or more
1.4 you will see the "count 1" on the logs twice

<img width="330" alt="Screenshot 2024-04-08 at 14 44 07" src="https://github.com/facebook/react/assets/16306521/943bff4c-ebf2-4465-8b6f-d999a2a97067">


2. By using your code:
2.1. Create a simple react project starter.
2.2 define a state of immutable value like number or string
2.3 define a trigger for updating state with new value by using button click event etc. for example if initial value is string "initial" then set this state to "second" on each click. 
2.4 add "console.log" above your return. 
2.5 click the button on the browser few times


https://codesandbox.io/p/sandbox/nervous-albattani-vl3mnm?file=%2Fsrc%2FApp.js%3A12%2C31

## The current behavior
it rerenders one more time with same old value. After one extra rerender, It won't rerender with same value as expected. 

## The expected behavior
it should never rerender with same prev value 
