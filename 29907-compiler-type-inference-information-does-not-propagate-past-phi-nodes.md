# [Compiler]: Type inference information does not propagate past phi nodes

> Issue #29907 - Created on 6/15/2024

> Original URL: https://github.com/facebook/react/issues/29907

## Description

### What kind of issue is this?

- [ ] React Compiler core (the JS output is incorrect, or your app works incorrectly after optimization)
- [ ] babel-plugin-react-compiler (build issue installing or using the Babel plugin)
- [ ] eslint-plugin-react-compiler (build issue installing or using the eslint plugin)
- [ ] react-compiler-healthcheck (build issue installing or using the healthcheck script)

### Link to repro

https://playground.react.dev/#N4Igzg9grgTgxgUxALhAMygOzgFwJYSYAEAwhALYAOhCmOAFMJQIwC+AlEcADrFEA2CHEQDa-CAEMAJnkwBzADREwQgDKSZ8gLpEAvESgqAyjgk4E9NBP4r2vIgKGiIOABYIYSlTgDybjzr6hggmZhZWNgh2mPaOwpDkCABqEjAA3LF4aET0LJw8fA4Jyal6ymoasnIZfKxECJFcsUUUJTBl3n7u6bGsvLGCwjAIYB2tKT18wziwxMNgNX2YIKxAA

### Repro steps

The following output is obtained after the InferTypes pass.

```javascript
...
bb1 (block):
  predecessor blocks: bb2 bb3
  someVar$51:TFunction<BuiltInSetState>: phi(bb2: someVar$46, bb3: someVar$49)
  [19] <unknown> $52 = LoadLocal <unknown> someVar$51
  [20] <unknown> $54 = StoreLocal Let <unknown> res$53 = <unknown> $52
  [21] <unknown> $55 = LoadLocal <unknown> res$53
  [22] Return <unknown> $55
```

I would expect the type (`TFunction<BuiltInSetState>`) of `someVar$51` phi node to propagate at instruction 19 but it does not happen.

I was able to figure out why it happens. During SSA generation the phi node's identifier has a `typeId` which is different than the identifier at instruction 19.

I tried to fix this by adding the following patch (to be run right after enterSSA pass) which just makes sure in such cases we always use the same `typeId`: 

```javascript
  // Ensure PHI node types are the same as their uses
  let ssaTypeRemap: Map<IdentifierId, Type> = new Map()
  for (const [_, block] of func.body.blocks) {
    block.phis.forEach(p => {
      ssaTypeRemap.set(p.id.id, p.type);
    })
  }
  for (const [_, block] of func.body.blocks) {
    for (const instr of block.instructions) {
      mapInstructionOperands(instr, (place) => {
        if (ssaTypeRemap.has(place.identifier.id)) {
          place.identifier.type = ssaTypeRemap.get(place.identifier.id)!;
        }
        return place;
      });
    }
    mapTerminalOperands(block.terminal, (place) => {
      if (ssaTypeRemap.has(place.identifier.id)) {
        place.identifier.type = ssaTypeRemap.get(place.identifier.id)!;
      }
      return place;
    });
  }
```
With this patch however 6 testcases fail:

```bash
Failures:

FAIL: phi-type-inference-property-store
 >> Unexpected error during test: 
Expected fixture `phi-type-inference-property-store` to succeed but it failed with error:

Invariant: Invalid mutable range for scope. Scope @3 has range [0:18] but the valid range is [1:22]
FAIL: phi-type-inference-array-push
 >> Unexpected error during test: 
Expected fixture `phi-type-inference-array-push` to succeed but it failed with error:

Invariant: Invalid mutable range for scope. Scope @3 has range [0:19] but the valid range is [1:23]
FAIL: obj-literal-mutated-after-if-else
 >> Unexpected error during test: 
Expected fixture `obj-literal-mutated-after-if-else` to succeed but it failed with error:

Invariant: Invalid mutable range for scope. Scope @2 has range [0:16] but the valid range is [1:18]
FAIL: mutable-lifetime-loops
 >> Unexpected error during test: 
Expected fixture `mutable-lifetime-loops` to succeed but it failed with error:

/mutable-lifetime-loops.ts: cycle detected
FAIL: for-in-statement-continue
 >> Unexpected error during test: 
Expected fixture `for-in-statement-continue` to succeed but it failed with error:

/for-in-statement-continue.ts: cycle detected
FAIL: alias-while
 >> Unexpected error during test: 
Expected fixture `alias-while` to succeed but it failed with error:

/alias-while.ts: cycle detected
FAIL: meta-isms/repro-cx-assigned-to-temporary
```
1. The mutable range inference pass gets a weird range (I am not sure how starting location can be zero, I guessed that the mutable range must start at atleast instruction idx + 1).

2. inference fails with a cycle detected.

I would appreciate some insights, thank you.

### How often does this bug happen?

Every time

### What version of React are you using?

19
