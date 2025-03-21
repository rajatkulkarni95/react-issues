# [React 19] State dispatch get stuck during an async form action (bug?)

> Issue #29590 - Created on 5/26/2024

> Original URL: https://github.com/facebook/react/issues/29590

## Description

In react 19 latest beta (2024.05.25).

The state dispatched in a form action never get committed by React if the form action is pending.  The state only changed after the action completed.  I'm not sure if this something a bug or a rule must be followed.  It seems a bit surprising.

Let's say a naive component like this.

```tsx
function Demo() {
  const [state, setState] = useState("A");

  const [, submitAction, isPending] = useActionState(async () => {
    setState("B")
    await sleep(60 * 1000)
    setState("C")
  }, null);

  return (
    <form action={submitAction}>
      <span>{x}</span>
      <button type="submit">Submit</button>
    </form>
  );
}
```

One will only see the value `A` and continue seeing value `A` from a minutes after submission, then they will see `C`.  Value `B` was never printed on the screen.

This seems not really related to the hook but the form `action` prop. What I want to do is to trigger some async validation before I call the api from the `action`.  Sometimes, the validation resulted a warning that I want the component to enter a "confirmation" state, but I cannot do anything if the action is triggered by the action prop.  
 
