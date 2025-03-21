# Bug: Uncaught TypeError: can't access property "useState", dispatcher is null

> Issue #30520 - Created on 7/30/2024

> Original URL: https://github.com/facebook/react/issues/30520

## Description


### Problem
Calling `useState` within the root component of a self-contained HTML file produces the following errors:
1. `Warning: Invalid hook call. Hooks can only be called inside of the body of a function component.`
2. `Uncaught TypeError: can't access property "useState", dispatcher is null`

Browsers tried: Firefox Developer Edition, Chromium, Firefox

Operating system: Arch Linux
 
#### Minimal Reproducible Example
<details>
<summary>HTML "file" containing minimal reproducible example</summary>


```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="en-US">
  <head>

    <script crossorigin src="https://unpkg.com/react@18.3.1/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js"></script>

    <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>

    <script type="text/babel" defer>

      function MyComponent() {
        const [num, setNum] = React.useState(0)

        return (
          <div>
            hello
          </div>
        )
      }

      const reactAppEntryPointElement = ReactDOM.createRoot(document.getElementById('react-app-entrypoint'));
      reactAppEntryPointElement.render(MyComponent());
    </script>
  </head>
  <body>

    <div id="react-app-entrypoint"></div>

  </body>
</html>
```
</details>

### Interesting note
Calling `useState` in a nested component produces zero errors

<details>
<summary>HTML "file" containing nested component which works correctly</summary>

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="en-US" xml:lang="en-US">
  <head>

    <script crossorigin src="https://unpkg.com/react@18.3.1/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js"></script>

    <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>

    <script type="text/babel" defer>

      function MyComponent() {

        return (
          <div>
            <MyNestedComponent />
          </div>
        )
      }

      function MyNestedComponent() {
        const [num, setNum] = React.useState(0)

        return <div>Nested</div>
      }

      const reactAppEntryPointElement = ReactDOM.createRoot(document.getElementById('react-app-entrypoint'));
      reactAppEntryPointElement.render(MyComponent());
    </script>
  </head>
  <body>

    <div id="react-app-entrypoint"></div>

  </body>
</html>

```
</details>

React version: 18.3.1

## Steps To Reproduce

1. Copy/paste the above HTML "file" into an actual file
1. Open the file in your browser. 

## The current behavior
The page loads a blank screen with errors in the browser console. I list the errors in the "Problem" section

## The expected behavior
The page should render a div with the text "hello" without displaying errors in the browser console
