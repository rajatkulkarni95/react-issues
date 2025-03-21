# [React 19] Cannot assign to readonly property

> Issue #30172 - Created on 7/1/2024

> Original URL: https://github.com/facebook/react/issues/30172

## Description

## Summary

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

I'm using https://waku.gg to use react components. I was trying to upgrade to the latest 19 rc and I started getting getting this error:

![image](https://github.com/facebook/react/assets/1192452/c8452687-af93-48cf-a549-5cb20d6354ed)

I boiled down the app into just a few file to demonstrate the issue [here](https://github.com/hipstersmoothie/waku-repro/)

The issue is as follow:

```tsx
// Client context Provider
import { StoryContextProvider } from "../../components/Context";
// Server Component
import A11yDecorator from "../../A11yDecorator";
// Client Component
import CenteredDecorator from "../../CenteredDecorator";

export default function Iframe() {
  const page = {};

  return (
    <StoryContextProvider value={{ page }}>
      <CenteredDecorator page={page}>
        <A11yDecorator page={page}>
          foo
        </A11yDecorator>
      </CenteredDecorator>
    </StoryContextProvider>
  );
}
```

Some observations:

- If I switch the order of `A11yDecorator` and `CenteredDecorator`, the app renders
- If I don't use a shared `page` variable and just pass objects to the relevant places, the app renders
- If I spread the `page` and make an new object when passing to the relevant places, the app renders

