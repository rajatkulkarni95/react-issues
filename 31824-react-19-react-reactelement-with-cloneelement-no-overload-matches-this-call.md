# [React 19] React.ReactElement with cloneElement - No overload matches this call.

> Issue #31824 - Created on 12/18/2024

> Original URL: https://github.com/facebook/react/issues/31824

## Description

As far as I know, `React.ReactElement` changed from `any` to `unknown` in React 19. I worked for most of the year with canary versions of Next and React where everything was typed correctly, but it seems that the type change was a more recent addition?

```
    "next": "^15.1.0",
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "@types/react": "^19.0.1",
    "@types/react-dom": "^19.0.2",
```

My case: After upgrading my application to the most recent versions, I get type errors for `React.ReactElement` used in React's `cloneElement` method. So I have a type which defines an element:

```
type Item = {
  icon: React.ReactElement;
};
```

And I use it in `cloneElement` where I also provide a `className`:

```
{cloneElement(navItem.icon, {
  className: "h-5 w-5",
})}
```

Here I get the type error: `No overload matches this call. Object literal may only specify known properties, and 'className' does not exist in type 'Partial<unknown> & Attributes'.`

So if I remove the `className` everything works fine.

```
{cloneElement(navItem.icon)}
```

I tried using `React.ReactNode` and `isValidElement` as guard, but it led me to the same type error. How would I solve this in React 19?

Not sure if it is related to this issue: https://github.com/facebook/react/issues/31357


![Screenshot 2024-12-17 at 21 51 19](https://github.com/user-attachments/assets/6cdec79b-52cf-4f08-9c3b-036d6e4b70ef)

