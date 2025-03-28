# [Compiler Bug]: `"use no memo"` Directive ignored by React Compiler Playground

> Issue #31331 - Created on 10/23/2024

> Original URL: https://github.com/facebook/react/issues/31331

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [x] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAwhALYAOhCmOAFAJRHAA6xRrIUYCRmEIuQTkIXANzsiROITA4iAbVlYcAGiK8cZVQF0iAXiI8EAZRwBDHAnoAGRpI4wEOWMQA8AEzwA3AHzAKnQAvu4A9N7+jsEgwUA

### Repro steps

To reproduce the issue, create a simple React component and add the `"use no memo"` directive at the top of the function, like this:
```jsx
function Component() {
  "use no memo";
  const [count, setCount] = useState(0);
  return <div>{count}</div>;
}
```
Even though the directive is there, the component still gets compiled, which shouldn’t happen according to the documentation. I’ve also tried placing the directive at the top of the file, and the behavior doesn't change.

To confirm, I tested this in different components and even in a fresh project, but the components keep getting compiled regardless of the directive.

The same result appears in the React Compiler Playground, showing that the `"use no memo"` directive is being ignored.


### How often does this bug happen?

Every time

### What version of React are you using?

19

### What version of React Compiler are you using?

19.0.0-beta-8a03594-20241020
