# Tttyyaja

> Issue #32387 - Created on 2/15/2025

> Original URL: https://github.com/facebook/react/issues/32387

## Description

.log(1)` inside a lifecycle method or a useEffect hook rather than placing it directly in the compobody. In React, code in the function body runs during rendering, which means it can be affected by optimizations like Fast Refresh or re-renders. This might explain why the log disappears when reopening Developer Tools. Instead, use:
> 
> ;
> 
> function App() {
>   useEffect(() => {
>     console.log(1);
>   }, []);
> 
>   return (
>     <div>
>       <img src="https://cdn.example.com/u%CE%B1%AA%E1%BC%E1%B2%E1%AB%CE%B1%E1%A7%E1_600x600.png" />
>     </div>
>   );
> }
> ```
> 
> This ensures that the log runs reliably when the component mounts and is not affected by render cycles. This ensures fundamental react principles are utilized ensuring predictable outcomes. I'm open to hearing from you more on this :) 

 _Originally posted by @shehryardev in [#32380](https://github.com/facebook/react/issues/32380#issuecomment-2660809275)_
