# Bug: Inline style backgroundImage and css property background-image are casuing browsers like Firefox and Chrome to abort the loading of the image(both browsers tested).

> Issue #27855 - Created on 12/25/2023

> Original URL: https://github.com/facebook/react/issues/27855

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: 18.2.0 

## Steps To Reproduce

1. Create a simple website using command `npx create-react-app`
2. Make a simple div and try to add the inline style to it `style={{ backgroundImage: url(${BusInterior1}), backgroundSize: 'no-repeat'}}`

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

Since its very simple I'd paste it here.
```
const HomePage = () => {
    return (
        <>  
            <div className="hero" style={{ backgroundImage: `url(${image})`, backgroundSize: 'no-repeat'}}>
            </div>    
        </>
    );
}
export default HomePage;

```

## The current behavior
Firefox showing `NS_BINDING_ABORTED` the size of image is literally 400Kb.

## The expected behavior
It should show the image without problems.
