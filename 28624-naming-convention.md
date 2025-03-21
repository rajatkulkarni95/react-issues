# Naming convention

> Issue #28624 - Created on 3/24/2024

> Original URL: https://github.com/facebook/react/issues/28624

## Description

Hello to everyone! I know that naming convention for the React components are not fixed, but I have situation that confuse me. I want my projects to have multiple different buttons. I prefer using BEM naming convention, but I don't know is it good to use for Component naming or just for CSS className? For me, the following will be acceptible:

```
project/
├── src/
│   ├── components/
│   │   ├── Button/
│   │   │   ├── Button--1.jsx
│   │   │   ├── Button--2.jsx
│   │   │   └── Button--3.jsx
```

I saw it quite frequently that people use something like "PrimaryButton", "SecondaryButton", but for me this look inexhaustible -> for me better will be "ButtonPrimary", "ButtonSecondary" since the "Button" is BASE.

Also, should BLOCK be used in naming convention instead of MODIFIER, like:
```
project/
├── src/
│   ├── components/
│   │   ├── Button/
│   │   │   ├── Form__button.jsx
│   │   │   ├── Sidebar__button.jsx
│   │   │   └── Footer__button.jsx
```
