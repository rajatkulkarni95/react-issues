# [React 19]Can the server support AsyncGenerator function in useActionState? 

> Issue #31382 - Created on 10/30/2024

> Original URL: https://github.com/facebook/react/issues/31382

## Description

I saw somewhere that useActionState fn supports the yield method, which will append the yield return data to the state array. Later I couldn't find it anymore.

Business scenario:
An action contains multiple third-party requests, and we need to promptly feedback the current status to the user.

I tried it today, and the code can run, but it reports an error. The server only supports the Promise method.

## Ideal code

```TypeScript
// actions.ts
'use server'

export async function* manyRequestsAction() {
  try {
    yield { index: 1, message: 'Step1', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 2, message: 'Step2', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 3, message: 'Step3', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 4, message: 'Step4', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 5, message: 'Step5', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 6, message: 'Step6', error: null }
    await new Promise((resolve) => setTimeout(resolve, 1000))
    yield { index: 7, message: 'Step7', error: null }
  } catch (e) {
    console.error(e)
    return { index: undefined, message: undefined, error: e.message }
  }
}

```

```TypeScript
// page.tsx
'use client'

type PageProps = {}

const Page = ({}: PageProps) => {
  const [currentStep, setCurrentStep] = useState<{
    index: number | null | undefined
    message: string | null | undefined
    error: string | null | undefined
  }>({ index: 0, message: null, error: null })
  const [loading, setLoading] = useState<boolean>(true)
  const [state, formAction] = useActionState(manyRequestsAction, undefined)
  useEffect(() => {
    const stepItr = async () => {
      const next = await state?.next()
      const value = next?.value
      const done = next?.done
      if (done) {
        return
      }
      setCurrentStep({ index: value?.index, message: value?.message, error: value?.error })
      console.log(value)
      stepItr()
    }
    if (state) {
      stepItr()
    }
  }, [state])
  return (
    <div>
      <p>
        Current Step Index: {currentStep?.index || 'No Index...'}
      </p>
      <p>
        Current Step Message: {currentStep?.message || 'No Message...'}
      </p>
      <p>
        Current Step Error: {currentStep?.error || 'No Error...'}
      </p>
      <button formAction={formAction}>Start</button>
    </div>
  )
}

export default Page

```

