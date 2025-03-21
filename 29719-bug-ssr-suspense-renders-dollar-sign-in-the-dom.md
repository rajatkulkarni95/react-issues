# [Bug] : SSR Suspense renders dollar sign ($) in the dom 

> Issue #29719 - Created on 6/2/2024

> Original URL: https://github.com/facebook/react/issues/29719

## Description

Hi I have tried to render a simple component via SSR. Which prints **$** sign because of that Hydration is failing.

React version: 18.3.2

## Steps To Reproduce

1. **App Component**

```
import React, { useEffect } from 'react'

interface Props {}

const App: React.FC<Props> = () => {
  useEffect(() => {
    console.log('App component mounted')
  }, [])
  return (
    <div>
      <h1>Hello, React</h1>
    </div>
  )
}

export default App
```
2. **express router**

```
router.get('*', (req, res) => {
      const Component = this.loadComponent(req.path)

      fs.readFile(
        path.resolve('./src/public/index.html'),
        'utf8',
        // eslint-disable-next-line consistent-return
        (error, data) => {
          if (error) {
            console.error(error)
            return res.status(500).send('An error occurred')
          }

          let didError = false

          const stream = renderToPipeableStream(
            <Suspense fallback={<div>Loading...</div>}>
              <Component />
            </Suspense>,
            {
              onShellReady() {
                res.statusCode = didError ? 500 : 200
                res.setHeader('Content-type', 'text/html')

                const initialHtml = data.replace(
                  '<div id="root"></div>',
                  '<div id="root">',
                )
                res.write(initialHtml)
                console.log(initialHtml)

                stream.pipe(res)
              },
              onShellError() {
                res.statusCode = 500
                res.send('<!doctype html><p>Loading...</p>')
              },
              onAllReady() {
                // If everything is ready, we end the stream
                if (!didError) {
                  res.end('</div></body></html>')
                }
              },
              onError(err) {
                didError = true
                console.error(err)
              },
            },
          )
        },
      )
    })

```
## The current behavior

![image](https://github.com/facebook/react/assets/13378125/b78b65c2-1f62-44a5-ae7e-41571f1e4d26)

$RC is appended in the dom which inserts the $ sign

![image](https://github.com/facebook/react/assets/13378125/ad058d64-ffe5-4672-95b9-1d219f0b9a49)


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->


## The expected behavior

Should print **Hello, React** only once without any additional characters .

