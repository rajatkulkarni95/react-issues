# How to access impure values during render (initially labeled as compiler bug)

> Issue #29765 - Created on 6/5/2024

> Original URL: https://github.com/facebook/react/issues/29765

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAggA5kAUAlEcADrFFyFg5EDaEOZANEWAQ4A8jwC6RALxEoggMo4AhjgSV6IddQDcjRkSIwhsYmqb6APAD49+2+YAmeAG7MANorBgAcooC2CSXU4RRh7dWszWwsAIygcHEIbKKjCAGFXPDgAa0lgGilLASFRKkoAWWUACwA6GEVMewhffIAqIgBGAAZO6mqEgDE8AA8Ee0oevogFGDxMAHMaagBfJOSI5OSAcSEiYQAVAAVVqPMAelj4wnXks8cna5O5SogAdyIXyoRMXIAhCAhXAh6pRuGRlg8bncIRtzJUAEyWfYHZB0UFLM7w6F2U5Q452XGRGFkLEbfpCOCfey7Q5ESjANG0ZR0TAIN4AEWUql6CQAMhBgoC9nh-NNZgtlniTqdiZKiLdnFizk9XhCztdtIwVphGAghmQIDB2BhsPhCERlS86TYPl9eDYKXhXPZDJg7UwEK55M83tJMFBXK43UsUQwmDbMCjov9AfUdEwHU6XSiAEpA3DVVOKXBeCD2BBx-Qer2vAD8KIAUnIABrVACigP8mHYAB8iH6A3GltQU2mcBnezm80RW+3XHQbIYcMZ3p9iCXmJVHc6vkQUUWEBbOyAlkA

### Repro steps

Using compiler version `0.0.0-experimental-938cd9a-20240601` in a Tauri/Vite React app.

I have a little app to parse OTPs from an e-mail, which would show the timestamp of when the OTP was retrieved.
Adding the compiler resulted in only the timestamp never changing while the OTP changed (minimal code to reproduce in the link).

<img width="243" alt="image" src="https://github.com/facebook/react/assets/10305085/33361774-0472-4ab3-a7c5-d40c77ecd73e">

I isolated the issue to this helper component:

```jsx
function Show({
  when,
  children,
  elseShow = null,
}: {
  when: boolean;
  children: React.ReactNode;
  elseShow?: JSX.Element | null;
}): React.ReactNode | null {
  return when ? children : elseShow;
}
```

Instead of using the `Show` component, if I just directly used a ternary it works in the compiler: 

```jsx
otp ?  (<> {/*show otp and timestamp*/} </>) : null
```

Am I doing something unusual in React or is this a compiler issue?

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc.0
