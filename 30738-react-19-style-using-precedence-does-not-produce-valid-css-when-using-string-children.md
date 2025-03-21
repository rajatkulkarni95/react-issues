# [React 19] style using precedence does not produce valid CSS when using string children

> Issue #30738 - Created on 8/18/2024

> Original URL: https://github.com/facebook/react/issues/30738

## Description

## Summary

Currently, the [style docs](https://react.dev/reference/react-dom/components/style#rendering-an-inline-css-stylesheet) showcase using a string with the style element like this:

```jsx
function PieChart({data, colors}) {
  const id = useId();
  const stylesheet = colors.map((color, index) =>
    `#${id} .color-${index}: \{ color: "${color}"; \}`
  ).join();
  return (
    <>
      <style href={"PieChart-" + JSON.stringify(colors)} precedence="medium">
        {stylesheet}
      </style>
      <svg id={id}>
        …
      </svg>
    </>
  );
}
```

However, this does not produce valid CSS, looking at the demo output in the docs example we can see this:

```
#:R2: .color-0: { color: &quot;red&quot;; }
```

Using `dangerouslySetInnerHTML` fixes the problem, but it would be nice to just be able to pass a string when using `precedence` or at least updating the docs to use `dangerouslySetInnerHTML` if that is the correct way.
