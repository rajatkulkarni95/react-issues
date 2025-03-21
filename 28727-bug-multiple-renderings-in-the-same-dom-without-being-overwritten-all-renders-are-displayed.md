# Bug: Multiple renderings in the same dom without being overwritten, all renders are displayed

> Issue #28727 - Created on 4/3/2024

> Original URL: https://github.com/facebook/react/issues/28727

## Description

In some cases, I need to render content multiple times in a DOM, and I expect the subsequent render to overwrite the previous content. However, in the code below, all the multiple render contents are displayed

React version: 18.2.0

## Steps To Reproduce
1. index.js
```js
import { createRoot } from 'react-dom/client';
import App from './App.js';
import './styles.css';
const dom = document.getElementById('root')

const render = (Comp)=> {
  createRoot(dom).render(Comp)
}
render(<App/>)
render(<App/>)

```
2. App.js
```js
import { useState,useEffect } from 'react';

export default function App() {
  const [show,setShow] = useState(false)
  useEffect(()=> {
    setTimeout(()=>{
      setShow(true)
    },500)
  },[])
  if(!show){
    return <></>    //  I found that when this place returns a non empty value, this problem will not occur anymore
  }
  return (
    <>
      <h1>Hello, world!</h1>
      <Counter />
    </>
  );
}
```
## The current behavior
The content of both renderings has been preserved
![image](https://github.com/facebook/react/assets/37828914/c6a00001-7b52-4897-8f1d-52d8462c4ed8)

## The expected behavior

Only the last one will be retained

