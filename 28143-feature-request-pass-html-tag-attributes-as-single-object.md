# feature request: Pass HTML tag attributes as single object

> Issue #28143 - Created on 1/28/2024

> Original URL: https://github.com/facebook/react/issues/28143

## Description

## The current behavior
Currently we're passing multiple attributes separately to ensure jsx compatibility with HTML like below 

```
<input type='text' name='firstName'/>

```

## The expected behavior

Could you please allow react to  pass the attributes of  an HTML tag in a single object like below. This shouldn't break the current behavior but as an additional feature. 
```
<input attributes={type:'text', name:'firstName'} />
```

