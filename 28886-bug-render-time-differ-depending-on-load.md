# Bug: render time differ depending on load

> Issue #28886 - Created on 4/21/2024

> Original URL: https://github.com/facebook/react/issues/28886

## Description

React version: 18.2.0

## Steps To Reproduce

1/ Create a heavy component to display 

can be simulated with something like:

`const HeavyComponent = () => {`
`  const start = performance.now()`
`  let i = 0;`
`  while (i < 9000000) {`
`    i = i + 1;`
`  }`
`  console.log('render time', performance.now() - start)`
`  return null;`
`};`
`
2/ force refreshing this component periodically with a setInterval. 

`const App = () => {`
`  // eslint-disable-next-line no-unused-vars`
`  const [_time, setTime] = useState(0);`
`  // setState in an interval to for refresh periodically`
`  useEffect(() => {`
`    const interval = setInterval(() => {`
`      setTime(_time => _time + 1);`
`    }, timeout);`
`    return () => clearInterval(interval)`
`  }, []);`
`  return <HeavyComponent />;`
`};`

**BUG**
Depending on the `timeout` configured (ie refresh frequency) the execution time of HeavyComponent differs (one to the double).

**Output in console:**
When putting a low timeout (10ms), the average render time is around 2.7 ms
When putting a high timeout (100ms), the average render time is around 6 ms
 
A very basic sample sample is available here (with the code I put on the ticket):
Link to code example: https://github.com/freeboub/ReactSampleForDevTool

## The current behavior
The execution time is not consistent depending on app load

## The expected behavior
The execution time should be consistent depending on app load

## additional informations
- I was investigating this issue in a react native project. -> issue highlighted with react dev tool.
- The result are consistent with profiler output (I can share screenshots if needed).
- Changing the HeavyComponent render time also gives consistent one to double refresh time.
- I was investigating this issue with profiler, but as console.log also highlight the issue, I kept it.
- There is maybe an explanation for this behavior, but was not able to find it in bugtracker nor on any other internet link.
- Same behavior observed with 
"react": "^19.0.0-canary-33a32441e9-20240418",
"react-dom": "^19.0.0-canary-33a32441e9-20240418", 

Thank you !

