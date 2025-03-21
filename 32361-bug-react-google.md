# Bug: react更新机制与google翻译机制导致的程序崩溃异常

> Issue #32361 - Created on 2/12/2025

> Original URL: https://github.com/facebook/react/issues/32361

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version: v18 v19 (mac, window)

## Steps To Reproduce

1. 网站 lang 设置成en
2. 网站 google 自动翻译 设置成 中文
3. 配合 
```javascript
const [flag, setFlag] = useState(false);

useEffect(() => {
  setTimeout(() => {
    setFlag(true);
  }, 8000);
}, []);

<span>
  <>
    {flag ? <div>测试</div> : <span>我说的</span>}
    {/* 出问题的下面这段代码 */}
    {flag ? "2" : "1"}
  </>
</span>
```
4. 注意：需要在flag更新之前，设置页面的google翻译为 中文

![Image](https://github.com/user-attachments/assets/426bdc8b-89ba-4910-81af-b5371ee62e62)

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

错误代码已上传至 github

https://github.com/zhangZzz-Free/react-bug

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The expected behavior

![Image](https://github.com/user-attachments/assets/50a41138-1065-4767-a55d-cf27a986a2ef)
