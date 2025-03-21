# Bug: in <StrictMode>, useEffect cleanup is called for the second mount, not the first one

> Issue #30835 - Created on 8/28/2024

> Original URL: https://github.com/facebook/react/issues/30835

## Description

Link to code example: https://playcode.io/1986248?v=2
React version: 18.0.0

I have a feeling that this was described one way or another, so I'll keep this one minimalistic and straight to the point.

Let's suppose we have some `Disposable` object we want to initialize when component mounts and destroy when component unmounts:

```
let globalCounter = 0;

const useCounter = () => {
  const [counter] = useState(() => globalCounter++);

  useEffect(() => {
    return () => {
      console.log('clean counter', counter);
    };
  }, []);

  return counter;
};
```

Let's render this component in strict mode, while looking at render/cleanup order (imports, createRoot and `<StrictMode> ` omitted):

```
function App() {
  const counter = useCounter();
  console.log('rendering counter', counter);

  return <div>current counter {counter}</div>;
}
```

## The current console output
```
rendering counter 0
rendering counter 1
clean counter 1           // why 1 and not 0?
```

And the App is obviously rendering div with `current counter 1`

## The expected console output

It's either first counter cleanup instead of the second one:
```
rendering counter 0
rendering counter 1
clean counter 0 // <-- this is different
```

Or the same, but before the second render:
```
rendering counter 0
clean counter 0 // <-- moved here
rendering counter 1
```

### The problem
The render proceeds with the second counter, which is "disposed", while the first counter is just "left hanging"

