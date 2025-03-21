# [React 19] Is precedene props for <link> works incorrectly?

> Issue #31621 - Created on 11/23/2024

> Original URL: https://github.com/facebook/react/issues/31621

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->
code sandbox - https://codesandbox.io/p/sandbox/currying-framework-fd5tfz

```
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
      <Low />
      <Medium />
      <High />
    </div>
  );
}

function High() {
  return <link rel="stylesheet" precedence="high" href="/high.css" />;
}

function Medium() {
  return <link rel="stylesheet" precedence="medium" href="/medium.css" />;
}

function Low() {
  return <link rel="stylesheet" precedence="low" href="/low.css" />;
}

```

according to [react conf](https://www.youtube.com/watch?v=AJOGzVygGcY)  high precedence link tag should be come before medium precedence in head tag,  but actually it renders as it declared in JSX

![스크린샷 2024-11-23 오후 11 31 44](https://github.com/user-attachments/assets/4e6cec3e-82a3-4e14-b5d9-422769a804e8)



[the document says](https://react.dev/reference/react-dom/components/link#controlling-stylesheet-precedence) 
> Stylesheets can conflict with each other, and when they do, the browser goes with the one that comes later in the document. React lets you control the order of stylesheets with the precedence prop. In this example, two components render stylesheets, and the one with the higher precedence goes later in the document even though the component that renders it comes earlier.

`higher precedence goes later` <- Is this meaning high precedence should be located after the lower precedence ?? 

Also, the documentation seems not so useful to understand how precedence works,

### Controlling stylesheet precedence example 
```tsx
import ShowRenderedHTML from './ShowRenderedHTML.js';

export default function HomePage() {
  return (
    <ShowRenderedHTML>
      <FirstComponent />
      <SecondComponent />
      ...
    </ShowRenderedHTML>
  );
}

function FirstComponent() {
  return <link rel="stylesheet" href="first.css" precedence="high" />;
}

function SecondComponent() {
  return <link rel="stylesheet" href="second.css" precedence="low" />;
}
```


### rendered html
```html
<html>
  <head>
    <link rel="stylesheet" href="first.css" data-precedence="high" />
    <link rel="stylesheet" href="second.css" data-precedence="low" />
  </head>
  <body>
    ...
  </body>
</html>
```

This example code's  `<FirstComponent/>` comes before `<SecondComponent/>` and rendered html  shows same it declared in JSX,  which is pretty obvious and has nothing to do with precedence, giving confusion. 



