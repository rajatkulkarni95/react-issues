# Bug: <Suspense> fallback is rendered inconsistently when there’s a hydration mismatch + the boundary suspends during hydration

> Issue #28285 - Created on 2/9/2024

> Original URL: https://github.com/facebook/react/issues/28285

## Description

React version: 18.2.0

## Steps To Reproduce

1. Create a tiny app that uses `<Suspense>` + suspends during hydration + has a hydration mismatch, for example:

   ```js
   hydrateRoot(
     document.getElementById('app'),
     <StrictMode>
       <Suspense fallback={<SuspenseFallback />}>
         <p>
           Hello from StackBlitz! <span>Hydration mismatch here</span>
         </p>
         <LinkThatSuspends />
       </Suspense>
     </StrictMode>
   );
   ```
  
   (Full code in [a StackBlitz](https://stackblitz.com/edit/stackblitz-starters-lrhtyy?file=src/style.css,public/index.html,src/index.tsx))
  
2. Load the app and observe that the suspense fallback is never mounted
3. Now, wrap the `<LinkThatSuspends />` element with a `<div>`:

   ```diff
   - <LinkThatSuspends />
   + <div><LinkThatSuspends /></div>
   ```
   
   ([StackBlitz](https://stackblitz.com/edit/stackblitz-starters-yrxvdn?file=src/style.css,public/index.html,src/index.tsx))

4. Load the app and observe that the suspense fallback is now mounted

Code example: [fallback not mounted](https://stackblitz.com/edit/stackblitz-starters-lrhtyy?file=src/style.css,public/index.html,src/index.tsx) · [fallback mounted](https://stackblitz.com/edit/stackblitz-starters-yrxvdn?file=src/style.css,public/index.html,src/index.tsx)

## The current behavior

The `<Suspense>` fallback is rendered inconsistently – depending on whether the element that suspends is wrapped with a `<div>`?!

## The expected behavior

The `<Suspense>` fallback is rendered either never, or always, no matter if the element that suspends is wrapped with anything.
