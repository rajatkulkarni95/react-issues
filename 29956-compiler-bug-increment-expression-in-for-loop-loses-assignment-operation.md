# [Compiler Bug]: Increment expression in for-loop loses assignment operation

> Issue #29956 - Created on 6/20/2024

> Original URL: https://github.com/facebook/react/issues/29956

## Description

### What kind of issue is this?

- [X] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAGgBQCURwAOsUWhDEWQDYI5F5EC8RADAG4uRADxEAjPyEi+3ANSSqwAL50VIFUA

### Repro steps

In our repo we have code similar to the Playground link posted above which when compiled loses the assignment part of the increment expression.

The original code:
```
          for (
            let node: LexicalNode | null = selection.anchor.getNode();
            node && !$isRootNode(node);
            node = node.getParent()
          ) {
```

Compiled to this code:
```
        for (let node5 = selection.anchor.getNode(); node5 && !$isRootNode2(node5); node5.getParent()) {
```

Happy to provide additional information or context if needed, thanks!

### How often does this bug happen?

Every time

### What version of React are you using?

19.0.0-rc-f3e09d6328-20240612
