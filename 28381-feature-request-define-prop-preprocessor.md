# Feature request: Define prop preprocessor

> Issue #28381 - Created on 2/20/2024

> Original URL: https://github.com/facebook/react/issues/28381

## Description

Today, React already 'preprocesses' some props for all components. For example, the 'style' prop accepts a CSSProperties object to handle styles more conveniently. It proves to be very useful in development

Why not go further and allow developers to define any preprocessable property? And let this prop have access to the DOM of the element, to accomplish whatever is needed

It could be useful for certain purposes. Today, currently React preprocesses all properties like onClick, onFocus, which are already native browser events. If we could define, we could include preprocessing for custom events
