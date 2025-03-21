# [React 19] Inconsistent hoisting behavior between links created with  `preload()` and manually inserted ones

> Issue #31352 - Created on 10/25/2024

> Original URL: https://github.com/facebook/react/issues/31352

## Description

## Summary

When trying to preload the `srcset` of an image with a `link` tag.  I found an unexpected behavior.

### Examples

#### Preloading srcset with `preload()`

``` js
preload('https://sample.com/foo', {
  as: 'image',
  imageSrcSet: 'https://sample.com/foo 1x',
});
```
##### Results (As expected)

``` html
<html>
  <head>
    <link rel="preload" as="image" imagesrcset="https://sample.com/foo 1x" />
  </head>
  <body></body>
</html>
```
#### Preloading srcset with `<link >`

``` html
<link
  rel="preload"
  as="image"
  imageSrcSet="https://sample.com/foo 1x"
/>
```
##### Expected

``` html
<html>
  <head>
    <link rel="preload" as="image" imagesrcset="https://sample.com/foo 1x" />
  </head>
  <body></body>
</html>
```
##### Current

``` html
<html>
  <head></head>
  <body>
    <link rel="preload"  as="image" imagesrcset="https://sample.com/foo 1x" />
  </body>
</html>
```

#### Preloading src with `preload()`

``` js
preload('https://sample.com/foo', {
  as: 'image',
});
```
##### Results (As expected)

``` html
<html>
  <head>
    <link rel="preload" as="image" href="https://sample.com/foo" />
  </head>
  <body></body>
</html>
```

#### Preloading src with `<link >`

``` html
<link
  rel="preload"
  as="image"
  href="https://sample.com/foo"
/>
```
##### Results (As expected)

``` html
<html>
  <head>
    <link rel="preload" as="image" href="https://sample.com/foo" />
  </head>
  <body></body>
</html>
```

#### Rendering `<img /> with srcset`

``` html

<img src="https://sample.com/bar" srcSet="https://sample.com/bar 1x" />
```
##### Results (As expected)

``` html
<html>
  <head>
    <link rel="preload" as="image" imagesrcset="https://sample.com/foo 1x" />
  </head>
  <body>
    <img src="https://sample.com/bar" srcset="https://sample.com/bar 1x" />
  </body>
</html>
```

Is this intended? Why links created with `preload()` end up hoisted to the head, while manually inserted links without the `href` attribute do not?

