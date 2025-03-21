# Bug: Updater function of set state in promise.then clause of useEffect are called twice and replacing state before promise.then doesn't work as expected.

> Issue #29829 - Created on 6/10/2024

> Original URL: https://github.com/facebook/react/issues/29829

## Description

I'm encountering an issue where the updater function of set state within promise.then of useEffect hook is being called twice. Additionally, attempting to replace the state before a promise resolves and then setting the state after the promise resolves does not work as expected. This behavior contradicts the behavior described in the [React documentation on queueing a series of state updates](https://react.dev/learn/queueing-a-series-of-state-updates#).

React version: 18.2

## Steps To Reproduce

Code
https://codesandbox.io/p/sandbox/sad-smoke-fzm9ww
```
const Context = createContext({})

const ChildWithCount = () => {
  const [num, setNum] = useState(1)
  const { l, setL } = useContext(Context)
  const [loading, setLoading] = useState(false)
  console.log("ChildWithCount re-renders", )

  useEffect(() => {
    console.log("useEffect")
    setLoading(true)
    setL([])
    new Promise((resolve) => {
      resolve()
      // setTimeout(() => resolve(), 100)
    }).then(() => {
      setL((prev) => {
        console.log("prev", prev)
        return [...prev, ...[1, 2, 3]]
      })
    }).finally(() => {
      setLoading(false)
    })
  }, [num])

  return (
    <div>
      <button
        onClick={() => {
          setNum((n) => n + 1)
        }}
      >
        Update
      </button>
      <ul>
        {l.map((_, index) => {
          return <li key={index}>{_}</li>
        })}
      </ul>
    </div>
  )
}

const App = () => {
  console.log("App rerenders")
  const [l, setL] = useState([])
  const contextValue = { l, setL }
  return (
    <Context.Provider value={contextValue}>
      <ChildWithCount />
    </Context.Provider>
  )
}

```
2. Run the code

## The current behavior
In strict mode, the first rendering lead to double data (6 items) in the List, even though I reset the list before calling the promise function, it didn't work. By clicking the `Re-fetch` button, the list being normal with 3 items. But I noticed that not matter if its strict mode, the list was replaced twice by checking console logs that the `console.log` in then clause are called twice and the list also changes twice with a quick flash of 6 items then showing the expected 3 items.


## The expected behavior
The initial list should only show 3 items and clicking the `Re-fetch` button shouldn't make the element flickering.
