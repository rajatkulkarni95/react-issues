# Bug: ForwardRef components cant have display names or types

> Issue #30068 - Created on 6/24/2024

> Original URL: https://github.com/facebook/react/issues/30068

## Description

I am developing a nested component and children pass events to parent components. I need to inject props to what user decides to put as children. Code example:
```
<ParentComponent>
  <ChildComponent>
    <ChildItemComponent><h1>Hello</h1></ChildItemComponent>
    <ChildItemComponent><h2>World</h2></ChildItemComponent>
  </ChildComponent>
</ParentComponent>
```
There are information exchange from ParentComponent to children via ContextProvider but we need some state change in parent component if children is clicked. I have done this using React.Children.map() and i check if the type of child is ChildComponent, then I clone it and inject update event handlers to the children.
The problem arise because ChildItemComponent needs ref to be passed into it and it is enclosed by forwardRef. This means I have no name to compare if the mapped component type is ChildItemComponent:
```
if (React.isValidElement<ChildItemComponentProps>(elm) && elm.type.toString() === ChildItemComponent.toString()) {
        return React.cloneElement<ChildItemComponentProps>(child, { onChange: setActiveTabByClick });
      }
```
As you can see I am using `toString` method to make what I need but I expect it to have displayName, a more efficient way. I could not find a way that I can set displayName for a forwardRef component.

I apologize in advance if there is a way that I could not find via my searches.

React version:18.2.0

## Steps To Reproduce
try to set display name for a ForwardRef component.

Link to code example:
[https://github.com/mehrizi/scrolling-tabs](https://github.com/mehrizi/scrolling-tabs)

## The current behavior
You cannot set displayName for a forwardRef component

## The expected behavior
You should be able to!
