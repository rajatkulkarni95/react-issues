# [React 19] new compiler handle the memoization of a function used in useEffect

> Issue #31925 - Created on 12/27/2024

> Original URL: https://github.com/facebook/react/issues/31925

## Description

previously:

const Component = () => {
  const [count, setCount] = useState(0);

  const handleAction = useCallback(() => {
    console.log(count);
  }, [count]);

  useEffect(() => {
    handleAction();
  }, [handleAction]);

  return <button onClick={() => setCount((prev) => prev + 1)}>Increment</button>;
};

in react 19 with the new compiler. can i write it simpler like: 

const Component = () => {
  const [count, setCount] = useState(0);

  const handleAction = () => {
    console.log(count);
  };

  useEffect(() => {
    handleAction();
  }, [handleAction]);

  return <button onClick={() => setCount((prev) => prev + 1)}>Increment</button>;
};

and the new compiler handle the memoization of handleAction function ?


