# Bug:  Input of type number is incrementing/decrementing on mouse scroll

> Issue #28885 - Created on 4/21/2024

> Original URL: https://github.com/facebook/react/issues/28885

## Description


React version:

## Steps To Reproduce
 Hey, I'm using a input field of type number. When the input field is in focus and mouse scroll is done , the value changes. This is happening only in chrome/safari but not in Firefox.
  So, i raised a [bug in chromium](https://issues.chromium.org/issues/334994023). I also attached a [reproducible example](https://lit.dev/playground/#project=W3sibmFtZSI6ImluZGV4Lmh0bWwiLCJjb250ZW50IjoiPCFET0NUWVBFIGh0bWw-XG48aGVhZD5cbiAgPHNjcmlwdD5jb25zb2xlLmNsZWFyKCk7PC9zY3JpcHQ-XG4gIDxzdHlsZT5cbiAgICA6cm9vdCB7IFxuICAgICAgZm9udC1mYW1pbHk6IHN5c3RlbS11aTtcbiAgICB9XG4gICAgXG4gICAgYm9keSB7XG4gICAgICBoZWlnaHQ6IDMwMHZoO1xuICAgICAgYmFja2dyb3VuZDogbGluZWFyLWdyYWRpZW50KHRvIGJvdHRvbSwgYmVpZ2UsIHRvbWF0bylcbiAgICB9XG4gICAgXG4gICAgLmNvbnRyb2xzIHtcbiAgICAgIHBvc2l0aW9uOiBmaXhlZDtcbiAgICB9XG4gICAgXG4gICAgZm9ybSB7XG4gICAgICBwb3NpdGlvbjogZml4ZWQ7XG4gICAgICBzY2FsZTogMztcbiAgICAgIHRvcDogNTB2aDtcbiAgICAgIGxlZnQ6IDUwdnc7XG4gICAgICB0cmFuc2xhdGU6IC01MCU7XG4gIDwvc3R5bGU-XG48L2hlYWQ-XG48Ym9keT5cbiAgPGRpdiBjbGFzcz1cImNvbnRyb2xzXCI-XG4gICAgPGJ1dHRvbiBpZD1cIndoZWVsQnV0dG9uXCI-QWRkIFdoZWVsPC9idXR0b24-XG4gIDwvZGl2PlxuICA8Zm9ybT5cbiAgICA8ZGl2PlxuICAgICAgPGlucHV0IHR5cGU9XCJudW1iZXJcIiB2YWx1ZT0wPlxuICAgIDwvZGl2PlxuICA8L2Zvcm0-XG4gIDxzY3JpcHQ-XG4gICAgY29uc3QgbGlzdGVuZXIgPShlKSA9PiB7XG4gICAgICBjb25zb2xlLmxvZygnd2hlZWwnKVxuICAgIH07XG4gICAgbGV0IHdoZWVsID0gZmFsc2U7XG4gICAgY29uc3QgY29udGFpbmVyID0gZG9jdW1lbnQ7XG4gICAgd2hlZWxCdXR0b24uYWRkRXZlbnRMaXN0ZW5lcignY2xpY2snLCAoZSkgPT4ge1xuICAgICAgd2hlZWwgPSAhd2hlZWw7XG4gICAgICBlLnRhcmdldC50ZXh0Q29udGVudCA9IHdoZWVsID8gYFJlbW92ZSBXaGVlbGAgOiBgQWRkIFdoZWVsYDtcbiAgICAgIGlmICh3aGVlbCkge1xuICAgICAgICBjb250YWluZXIuYWRkRXZlbnRMaXN0ZW5lcignd2hlZWwnLCBsaXN0ZW5lcik7XG4gICAgICB9IGVsc2Uge1xuICAgICAgICBjb250YWluZXIucmVtb3ZlRXZlbnRMaXN0ZW5lcignd2hlZWwnLCBsaXN0ZW5lcik7ICAgIFxuICAgICAgfSAgICAgIFxuICAgIH0pO1xuICA8L3NjcmlwdD5cbjwvYm9keT5cbiJ9LHsibmFtZSI6InBhY2thZ2UuanNvbiIsImNvbnRlbnQiOiJ7XG4gIFwiZGVwZW5kZW5jaWVzXCI6IHtcbiAgICBcImxpdFwiOiBcIl4zLjAuMFwiLFxuICAgIFwiQGxpdC9yZWFjdGl2ZS1lbGVtZW50XCI6IFwiXjIuMC4wXCIsXG4gICAgXCJsaXQtZWxlbWVudFwiOiBcIl40LjAuMFwiLFxuICAgIFwibGl0LWh0bWxcIjogXCJeMy4wLjBcIlxuICB9XG59IiwiaGlkZGVuIjp0cnVlfV0) there. 
  They said it is a intended behavior describe in https://chromestatus.com/feature/6662647093133312 and we just need to use `useCapture` where the wheel event is attached. But , I can see the wheel event is attached by react in the root element automatically. So, how can I proceed here. Any suggestion would be much helpful. 
  
1. Open https://mui.com/joy-ui/react-input/#inner-html-input
2. Click on the type number input field and do mouse scroll. The input value changes and also the page scrolls.
3. Inspect and see the wheel event attached to the __next div element and also to the body
4. Remove the wheel event and see the issue no longer exists


Link to code example:
https://mui.com/joy-ui/react-input/#inner-html-input


## The current behavior

Cannot set useCapture parameter option to the events attached 
## The expected behavior
Need to set useCapture option to the events attached (or) remove wheel event from being attached
