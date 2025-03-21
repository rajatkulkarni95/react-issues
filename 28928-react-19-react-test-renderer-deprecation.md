# [React 19] react-test-renderer deprecation

> Issue #28928 - Created on 4/26/2024

> Original URL: https://github.com/facebook/react/issues/28928

## Description

## Summary

Today our team relies on react-test-renderer to render a JSON tree which is subsequently used for search indexing. By rendering to JSON we have a structure we can use to extract semantic data like `title`, `meta`, `description`, etc. To do something similar without `react-test-renderer` we'd have to render to HTML, and then use an HTML parser to parse and extract semantic data.

I realize that this is an "off label" use of React Test Renderer but I was hoping there would be an alternative to with `react-test-renderer`'s deprecation.

```tsx
ReactTestRenderer.create(reactElement).toJSON();
```
