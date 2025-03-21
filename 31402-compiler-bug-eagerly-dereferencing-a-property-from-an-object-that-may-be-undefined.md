# [Compiler Bug]: Eagerly dereferencing a property from an object that may be undefined

> Issue #31402 - Created on 11/2/2024

> Original URL: https://github.com/facebook/react/issues/31402

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgDMoA7OXASwhPwGEIBbbEhE3ACgEp9gAdG-HGpgCAbTgwImADT4wCXLUmYAuvgC8+AEoIAhuQB0UeQGVcu3Ai798g4QQpgAok1wBPDfgCEEqfxt2JCL41ABiEBCeXBoAfDwBthSE+Oxeji6Y7tx8Ara2hBHsvpgG6JwJ+AC+AdUkATAKsDTsFQA8ACYUAG4hJLQANhRwANbqwGERlfgA9DEB5SS1IJVAA

### Repro steps

```js
export function Component() {
  const [crop, setCrop] = React.useState()
  const isEmpty = !crop

  const onFoo = () => {
    if (!isEmpty) {
      foo(crop.x)
    }
  }

  return (
    <div onClick={onFoo} />
  )
}
```

We end up with 

```js
function Component() {
  const $ = _c(5);
  const [crop] = React.useState();
  const isEmpty = !crop;
  let t0;
  if ($[0] !== isEmpty || $[1] !== crop.x) {
    t0 = () => {
      if (!isEmpty) {
        foo(crop.x);
      }
    };
    $[0] = isEmpty;
    $[1] = crop.x;
    $[2] = t0;
  } else {
    t0 = $[2];
  }
  const onFoo = t0;
  let t1;
  if ($[3] !== onFoo) {
    t1 = <div onClick={onFoo} />;
    $[3] = onFoo;
    $[4] = t1;
  } else {
    t1 = $[4];
  }
  return t1;
}
```

The original code isn't accessing `crop.x` when `isEmpty` is `true`, but the generated code does. So it fails with runtime crash. Turning off the compiler fixes it.

### How often does this bug happen?

Every time

### What version of React are you using?

18

### What version of React Compiler are you using?

19.0.0-beta-6fc168f-20241025
