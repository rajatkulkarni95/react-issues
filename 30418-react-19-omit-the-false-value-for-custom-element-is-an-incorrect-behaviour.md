# [React 19] Omit the false value for custom element is an incorrect behaviour

> Issue #30418 - Created on 7/22/2024

> Original URL: https://github.com/facebook/react/issues/30418

## Description

## Summary

The false value could be selected by a attribute selector.

```html
<custom-element an-attr="false"></custom-element>
<style>
custom-element[an-attr="false"]:defined{
   background:pink;
}
</style>
```

