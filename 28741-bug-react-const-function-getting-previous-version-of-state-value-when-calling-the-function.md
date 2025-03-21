# Bug: React const function getting previous version of state value when calling the function.

> Issue #28741 - Created on 4/4/2024

> Original URL: https://github.com/facebook/react/issues/28741

## Description

<!--
  Hey hope all of you are well! I'm stuck, the react functional component const function getting the previous value of state when calling on button click. that's very wired because it's working fine but not the same code but getting this wired behaviour. 

Please help me to sort out. Thanks
-->

React version:
React: 18.2.0
React Dom: 18.2.0

Link to code example:
```
const [popup, setPopup] = useState(false);

  useEffect(() => {
    if (popup) {
      document.getElementById("email-popup").style.visibility = "visible";
      document.getElementById("email-popup").style.opacity = "1";
    } else {
      document.getElementById("email-popup").style.opacity = "0";
      document.getElementById("email-popup").style.visibility = "hidden";
    }
  }, [popup]);
  
  const onClose = () => {
    console.log("=====Clicked Before Update====", popup);
    setPopup(false);
    console.log("=====Clicked After Update====", popup);
  };
  
  return (
   <span onClick={() => onClose()}>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="18"
                height="18"
                fill="#777"
                viewBox="0 0 16 16"
              >
                <path d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z" />
              </svg>
            </span>
);
```

## The current behavior
Getting the old value for example. when try to call onClose function, in that function getting false value

## The expected behavior
Should be true value when call onClose function on button click. 
