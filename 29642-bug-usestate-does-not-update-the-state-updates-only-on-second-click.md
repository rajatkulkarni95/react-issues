# Bug: useState does not update the state. Updates only on second click

> Issue #29642 - Created on 5/29/2024

> Original URL: https://github.com/facebook/react/issues/29642

## Description

<!--
useState updates the state only on second click and it looks like it updates the state very slow. 
-->

React version:
  "react": "^18.2.0",
   "react-dom": "^18.2.0",
## Steps To Reproduce

   const [activeLink,setActiveLink]=useState('/home');
    const goTo = (link:string) => {
    setActiveLink((prev)=>prev=link);
    navigate(`/react-mini-tg${link}`);
};

Here it goes to another route, but fails to update the activeLink

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior


## The expected behavior

