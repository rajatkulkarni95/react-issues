# Bug: How do I synchronize my render function?

> Issue #30543 - Created on 7/31/2024

> Original URL: https://github.com/facebook/react/issues/30543

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
18.3.1
## Steps To Reproduce

       // 创建dom, msg的包裹器
        // 创建包裹容器
        const __container = document.createElement("div");
        const root = createRoot(__container);
        // 创建节点
        const wrapper = createElement(ContainerWrapper);
        // 渲染节点
        root.render(wrapper);
      
        document.body.appendChild(__container);
        // I cannot synchronize
        // I don't want to render the __container node on the page. How should I handle it? How can I synchronize my render function?
        setTimeout(() => {
          document.body.appendChild(__container?.firstElementChild);
          // 获取参数配置
          const normalized = handleOptions({ ...params, appendTo: `#${wrapId}` });
          return message({ ...normalized, type });
        });

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:
not have
<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior


## The expected behavior

