# Bug: submitting form clears fields unnecessarily despite using preventDefault

> Issue #27877 - Created on 1/4/2024

> Original URL: https://github.com/facebook/react/issues/27877

## Description

Submitting form clears fields unnecessarily despite preventDefault
React version: 18.2.0

## Steps To Reproduce

1. after loading the following code, type a number in the input field and click submit
2. expected result: value in input field does not change
3. actual result: input field becomes blank

```
import React, {useState, StrictMode } from 'react';
export default function SimpleSearch({forms}) {
	const [searchResults, setSearchResults] = useState([]);
	return(
		<StrictMode>
		<form method="POST" onSubmit={
			(e)=>
			{
				e.preventDefault();
				setSearchResults([]);
			}
		} >
		 <FilterCriteria/>
		<button className="submit_save"   type="submit" >Load Results</button>
				<button className="submit_cancel" type="reset" >Clear</button>
		</form>
		</StrictMode>
	)
	 function FilterCriteria(){
		 return (
		 <input  required={true} autoComplete="off" />
		 )
	 }
}
```

If the FilterCriteria component is inlined into the SimpleSearch component as shown below, the behavior is as expected (form values don't clear on submit with preventDefault)

```
import React, {useState, StrictMode } from 'react';
export default function SimpleSearch({forms}) {
	const [searchResults, setSearchResults] = useState([]);
	return(
		<StrictMode>
		<form method="POST" onSubmit={
			(e)=>
			{
				e.preventDefault();
				setSearchResults([]);
			}
		} >
		 <input  required={true} autoComplete="off" />
		<button className="submit_save"   type="submit" >Load Results</button>
				<button className="submit_cancel" type="reset" >Clear</button>
		</form>
		</StrictMode>
	)
}
```
