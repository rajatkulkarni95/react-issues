# [Compiler Bug]: Stripping curly braces breaks character escapes (breaks JSX spec 1.5.1)

> Issue #29648 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29648

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwAkIBbBACgEp8wADpt8MBLlhteo-PPwAeAHxyF8xQGVuCAMLdsdBHQK4MuALzAA5AEFhogKLWAvvgD0qseq079XQ2NTcwthEHsnMI8vH081fgBuURdREBcgA

### Repro steps

1. Use a string with a newline character (`\n`) passed as a prop to a component with curly braces `prop={"text\ntext"}`
2. Observe that react compiler outputs `prop="text\ntext"` instead of `prop={"text\ntext"}`

This is incorrect behavior. The newline character is no longer properly treated as a newline but rather as the raw text `\n`.

You can see this behavior be correctly also incorrectly handled in the second component, where `prop="text\ntext"` becomes `prop="text\\ntext"`, resulting in the wrong text being displayed on the screen.

JSX rules specifically don't allow this kind of conversion, noted in [1.5.1 of the spec](https://facebook.github.io/jsx/#sec-jsx-string-characters)

> Historically, string characters within [JSXAttributeValue](https://facebook.github.io/jsx/#prod-JSXAttributeValue) and [JSXText](https://facebook.github.io/jsx/#prod-JSXText) are extended to allow the presence of [HTML character references](https://facebook.github.io/jsx/#sec-HTMLCharacterReference) to make copy-pasting between HTML and JSX easier, at the cost of not supporting \ [EscapeSequence](https://tc39.es/ecma262/#prod-annexB-EscapeSequence) of ECMAScript's [StringLiteral](https://tc39.es/ecma262/#prod-StringLiteral).

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-6f23540c7d-20240528
