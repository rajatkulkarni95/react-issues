# [React 19] useActionState when firing the action multiple times doesn't behave like transition

> Issue #30777 - Created on 8/21/2024

> Original URL: https://github.com/facebook/react/issues/30777

## Description

using the below  code
```
const [data, action, isPending] = useActionState(
    async (currentState, formData) => {
      const name = formData.get('name')
      await new Promise(r => setTimeout(() => r(''), 3000))
      return name
    },
    null
  )
```
if i hit a button that submits  the action multiple times the result appears on the screen after very long time and some times never
