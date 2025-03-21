# [Compiler Bug]: Compiler generates unsafe property access code while updating cache

> Issue #31351 - Created on 10/24/2024

> Original URL: https://github.com/facebook/react/issues/31351

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvjiswBMEwDmdJmwC8+KGAQBlBUrpCA3OPH51m7mE4MAKmTABrfmImnaDZPiH4VAPhEnTQKYSTzlFZQA6GTJcDW8VNVFwXQRCAH1lJOFnQNz8AHp8-G44RDA5Onl8AAMwvQiNBBgIhABbMiZKaskKTTB8ACUEMkZ8AGEIVsxOpoC8gqLcCHwkuBGACwQk-FxN-BgEMCoCCBDdpn6RsrAAGnwAdyZd6AJdrZc8wvxMGAhcBEYLDYpx2e1quBiGm6cE2cHsAEJ8ABJNjnfoYMhTSgIG5zT5FaqNGDdR6USj4MiUe5kTj9ABGCHUdGIJGUqTudKgBCGIwIEymMxgeNyX3kCDoTRih1BF0kEGID3WTBhkhgdk2YGQwsCX1MABIANoARgAut58HVIkSWu1OkYPrkpHRINiIpQIPJ+EkdIpUvhlBSwEk7pa6A1NM02h1KIJtQBfPEJiRxwT2gIHWIwNgAHkITAAbj4ABIIMnLADqOEohGz+TzhftSfEbkBrDM2l0yi8OX9IX4j2ZEHu2QWxSpNP6uBgUEZAbROwgnHwGKx71yGdgbB7uWisU1KxA7rIecqwe1XwAqhH-f16PY6EO6CHlm8Djf8A-2zAKbgp0xOf8+CcAguDwomARJqYpaaP4HwblmsHzLuGgeEkdSpBkdBng6X4eMAy62pQqEgP8MgAAIrpgrpSK0B6QYE9FJk2dAtswbaNBYVhwLYDj8GQMDyGA2QBF8AAyHrKqCMQ9GSlwCWAEQtoGXHrL8D4aJQnB3LadAQso-S7ggETiHGIBxkAA

### Repro steps

Running the component in the playground link will always crash because React Compiler attempts to cache the result of a deep property access without the checks necessary in the original code. Explained in playground link!

### How often does this bug happen?

Every time

### What version of React are you using?

19 (playground)

### What version of React Compiler are you using?

19? (playground)
