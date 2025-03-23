# React compiler requires that expressions  referenced in handler code are always resolvable

> Issue #29127 - Created on 5/17/2024

> Original URL: https://github.com/facebook/react/issues/29127

## Description

I was trying to port a bigger existing code base to react-compiler.

I ran about the issue, that react-compiler requires all expressions used in event handlers to be always resolvable (even if the handler itself can not be reached in some cases).

Here is a very simplified sample:

````

const App = () => {
    return <div>
                <CompilerTest />
                <CompilerTest data={{id: 1}} />
              </div>
  }

const CompilerTest = ({data}) => {
  const handleTest= () => {
    console.log(data.id);
    }

  return <div>
             {data.?id &&
                <button onClick={handleTest}>Test</button>
                }
             </div>
  }
````
Replacing console.log(data.id) with console.log(data?.id) resolves the issue. 
But this would of course require to manualy find and update all of the affected handlers.

Wouldn't it be better if react-compiler uses the ?. instead of . for the dependencies?
   
