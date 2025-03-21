# The value of useReducer (proposal)

> Issue #28503 - Created on 3/6/2024

> Original URL: https://github.com/facebook/react/issues/28503

## Description

Hi!

This is not a bug. 
Please help me to understand the value of `useReducer`.

Let's take a look at the typical example:

```js
import React, { useReducer } from 'react';

interface CounterState {
  count: number;
}

type CounterAction =
  | { type: 'increment' }
  | { type: 'decrement' };

const initialState: CounterState = { count: 0 };

const reducer = (state: CounterState, action: CounterAction): CounterState => {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error('Unhandled action');
  }
};

const Counter: React.FC = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}

export default Counter;
```
Documentation says: https://react.dev/learn/extracting-state-logic-into-a-reducer#comparing-usestate-and-usereducer

> However, useReducer can help cut down on the code if many event handlers modify state in a similar way.

> `useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values. It also lets you optimize performance for components that trigger deep updates because you can pass `dispatch` down instead of callbacks.

Wouldn't it be easier to use just a JavaScript module to aggregate state logic?

```js
const myModule = {
  increment: (state) => {
    return {count: state.count + 1};
  },
    
  decrement: (state) => {
    return {count: state.count - 1};
  }
};

const Counter: React.FC = () => {
  const [state, setState] = useState(initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => setState(myModule.increment)}>Increment</button>
      <button onClick={() => setState(myModule.decrement))}>Decrement</button>
    </div>
  );
}
```

Benefits:
- no calling function by string
- no switch statement
- no conditional types (CounterAction)


