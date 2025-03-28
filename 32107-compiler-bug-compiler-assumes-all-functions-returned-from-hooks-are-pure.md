# [Compiler Bug]: Compiler assumes all functions returned from hooks are pure

> Issue #32107 - Created on 1/17/2025

> Original URL: https://github.com/facebook/react/issues/32107

## Description

### What kind of issue is this?

- [x] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhASwLYAcIwC4AEwBAwhAHZ4wQA2NCMANAVGAgGK4YEC+BAZtW4ByGAgCGcPAFoAFhAgBrafy7CA3AB1y2hAA8c+AgBME-cVBqF+UclLQUCAWQCenGBgAUASiLaCBHAUYITEQZTUNMyy4uTG9ADKUABGGGh4zADu4nhwsrwEALwsbO5exBgQpsgEwhQkMeQA5gjCzKbmlngAauI0UAhgNS14ACJmFla9-YM+vN5aOuQBNnZ4Dssj451TfQNgc8D+AQRieLDLR8snARiDYOItNcLCxwE8i+-ax6v2jhRJVLpTzGHLiXxXG7hSD0AB0NAgTRBYIWxx432uZwuBE8bwIAB5VB4CACUmk8IVgI14ghAeTPKSgXhvDwAHx4gL4sgRWj0GAck7kcR3SnCO5gB4tYTo643ALhKi0SkKyIyuUnGCWQaU4hiACOUDQYmMNSoA14avVpwQcQYlM8xH4aAQNGM8yKrJxApu+LQ5CwUFCsODTpdxj4AHp2bK5SyBVGBfjjGgAG7Rq1EABSCQA8gA5WEhGB+ppofguTzZXKyHxxmOciPJtN4-ERokYdMEVHkGUgHhAA

### Repro steps

The playground link is a **very** simplified example of a form using the [react-hook-form](https://github.com/react-hook-form/react-hook-form) library. The component is supposed to output the live value of the input in a div, by calling the [watch](https://react-hook-form.com/docs/useform/watch) function during render (this function returns the updated form values).  

This doesn't work after the compiler kicks in because it only **calls** the watch function if its **reference** changes, which is not the case. react-hook-form guarantees stability of this function accross renders. The relevant part of the compiled code is

```
 if ($[6] !== watch) {
    t4 = JSON.stringify(watch());
    $[6] = watch;
    $[7] = t4;
  } else {
    t4 = $[7];
  }
```

Is this an issue, or is it something that we should work-around in user land?

Thanks,
David

### How often does this bug happen?

Every time

### What version of React are you using?

react@19.0.0

### What version of React Compiler are you using?

babel-plugin-react-compiler@19.0.0-beta-e552027-20250112
