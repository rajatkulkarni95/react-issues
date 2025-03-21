# After using forwardRef in a JSX component, you encounter an error when using it in a TSX component.

> Issue #28823 - Created on 4/11/2024

> Original URL: https://github.com/facebook/react/issues/28823

## Description

Suppose I have such a JSX component.
```jsx
// jsx
import { forwardRef } from "react";

const Com= forwardRef(function (props) {
  return <div>{props.text}</div>;
});

export default Com;
```
And then using it in a TSX file.
```tsx
// tsx
export default function Page() {
  return (
    <div>
      <Com text="text" />
    </div>
  );
}
```
 will encounter this error.
不能将类型“{ ref: RefObject<HTMLDivElement>; text: string; }”分配给类型“IntrinsicAttributes & RefAttributes<any>”。
  类型“IntrinsicAttributes & RefAttributes<any>”上不存在属性“text”。

> Although I can convert the JSX component to TSX, I would prefer not to.
