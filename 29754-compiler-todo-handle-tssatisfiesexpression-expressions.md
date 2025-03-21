# [Compiler Todo]: Handle TSSatisfiesExpression expressions

> Issue #29754 - Created on 6/4/2024

> Original URL: https://github.com/facebook/react/issues/29754

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhHCA7MAXABAQ1wF5cBGXMfbASzADNqExcMoBbAIwRgG4AdDCAC+QA

### Repro steps

The compiler currently cannot handle `TSSatisfiesExpression`
```ts
const a = 1 satisfies number;
```
Results in
```
(BuildHIR::lowerExpression) Handle TSSatisfiesExpression expressions
```

I think adding support to the code itself would be pretty straignt-forward, as the typescript construct of `satisfies` can just be ignored and handled as the inner expression:
```ts
    case "TSSatisfiesExpression": {
      const expr = exprPath as NodePath<t.TSSatisfiesExpression>;
      return lowerExpression(builder, expr.get("expression"));
    }
```
https://github.com/facebook/react/compare/main...nikeee:react:handle-satisfies-expression?expand=1

However, when implementing this, it does not build, due to type conflicts of `@babel/types`. `npm ls @babel/types` suggests that there are multiple versions of `@babel/types` in use, some of which already support `satisfies` and others don't. `satisfies` was introduced in TS 4.9, which is [supported since babel 7.20.0](https://babeljs.io/docs/features-timeline#babel-7200).
The RC itself does depend on a lower version, but ^7.20 versions are included as a transitive dependency. This might be the reason why the parser does not throw an error, while RC cannot handle it (and BuildHIR doesn't know anything about that).
I also tried upgrading babel oin the entire project, but that seems to be not as trivial as I'd thought. Maybe there is a different solution.

### How often does this bug happen?

Every time

### What version of React are you using?

19
