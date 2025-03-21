# Bug: Hundreds render of Suspense child with hydration error

> Issue #29922 - Created on 6/18/2024

> Original URL: https://github.com/facebook/react/issues/29922

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

## React version: 18.2

## Description

Hello!

Found a few problem cases with Suspense, one quite exotic, one easy to reproduce, and in our project I get both at the same time.

### First case - **hundreds render of Suspense child with hydration error**.

If wrapped in Suspese component cause hydration error, React will render this component hungreds or event thousands times.

Example:

```tsx
function MissmatchCmp() {
  return <p>Missmatch Component {typeof window === 'undefined' ? 1 : 2}</p>
}

function App() {
  return (
    <>
      <Suspense>
        <MissmatchCmp />
      </Suspense>
    </>
  )
}
```

<img width="996" alt="Снимок экрана 2024-06-18 в 12 13 41" src="https://github.com/facebook/react/assets/15360667/0137d5a0-7382-4751-8eb6-207c3f19e2b6">

### Second case - **Looped render of class component with `setState` in constructor wrapped in Suspense**

Of course, `setState` in counstructor sounds like a bad pattern, but we have it in some big legacy class component.

Example:

```tsx
class CmpWithSetState extends React.Component {
  constructor(props) {
    super(props);

    // emulate state change after http call
    setTimeout(() => {
      this.setState({ foo: "bar" });
    // with increased timout loop can be prevented
    }, 25);
  }

  render() {
    return <p>CmpWithSetState</p>
  }
}

function App() {
  return (
    <>
      <Suspense>
        <CmpWithSetState />
      </Suspense>
    </>
  )
}
```

<img width="997" alt="Снимок экрана 2024-06-18 в 12 22 21" src="https://github.com/facebook/react/assets/15360667/47eae0d5-5238-4443-a9e5-26c92d9c3b31">

### Bingo case - **Both of previous examples in same component are guaranteed to cause a loop**

<img width="993" alt="Снимок экрана 2024-06-18 в 12 28 16" src="https://github.com/facebook/react/assets/15360667/492062d5-9e94-462e-8e7d-f72a853362da">

[profiling-data.18.06.2024.12-28-19.json.zip](https://github.com/user-attachments/files/15883664/profiling-data.18.06.2024.12-28-19.json.zip)

## Steps To Reproduce

1. Clone repo `https://github.com/SuperOleg39/react-ssr-perf-test`
2. Switch to branch `react-bug-suspense-child`
3. Run application build and server - `cd react-18-stream && yarn && yarn start` (use Node.js 16)
4. Open application page at `http://localhost:4000`

Link to code example:

https://github.com/SuperOleg39/react-ssr-perf-test/pull/1

## The current behavior

Components which are not really suspended, rendered multiple times, like React wait for promise to resolve.

Also looks like React treats this components both as one when check if they are suspended or not.

## The expected behavior

Expect the same behaviour as without `Suspense` boundary.

We use `Suspense` for our components mostly to prevent server rendering failure if one of this components failed.

