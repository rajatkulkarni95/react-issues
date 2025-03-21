# Bug: Hydration fails when async script is located outside head tag

> Issue #29801 - Created on 6/7/2024

> Original URL: https://github.com/facebook/react/issues/29801

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->
I have a nextjs application that have to render a json-ld schema. The easiest place to generate the schema was in a page component responsible for loading product. I though using the [special rendering behaviour of scripts](https://react.dev/reference/react-dom/components/script#special-rendering-behavior) will move the`<script>` tag from the `<body>` into the `<head>` section. I was testing with postman because I wanted to see only the initial version of the page and be sure that the script element is in the `<head>` section. Which wasn't. The problem was a client component that was rendering a loading screen and preventing everything underneath to be rendered on the server. I thought this is safe for now and tried to run the code in the browser which led to this error:

Update: The issue exist also when navigating to a page that has 
```javascript
...
  <script
        async
        src=' '
        type='application/ld+json'
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
...
```
using nextjs Link or router.push().

<img width="883" alt="Screenshot 2024-06-07 at 19 09 17" src="https://github.com/facebook/react/assets/3524687/b0fc4da4-a439-4ac7-8e04-14ef24cd8449">

It seems react is trying to create a missing dom element during hydration (I might be wrong) and in the process `setInitialProperties` is called with a wrong parameter - `link`  instead of `script`

```
        instance = ownerDocument.createElement('script');
        markNodeAsHoistable(instance);
        setInitialProperties(instance, 'link', scriptProps);
        (ownerDocument.head: any).appendChild(instance);
```

React version: 19.0.0-beta-26f2496093-20240514

## Steps To Reproduce
Scenario 1
1. clone the repo
2. npm i && npm run dev
3. `git checkout main`
4. navigate to http://localhost:3000
The loading screen is shown for 2 seconds. After that the page freeze and the error is shown in the console. The tab might snap in a bit because of it will run out of memery.

Scenario 2
1. clone the repo
2. npm i && npm run dev
3. `git checkout navigation-example`
4. navigate to http://localhost:3000
5. click 'Test Page' link
The page hangs right away with the same error in console

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example: https://github.com/atstoyanov/react-dom-bug

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior


## The expected behavior
The page renders and the `<script>` component is moved into the `<head>` section.
