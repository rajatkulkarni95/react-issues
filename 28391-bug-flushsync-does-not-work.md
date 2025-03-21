# Bug: `flushSync` does not work

> Issue #28391 - Created on 2/21/2024

> Original URL: https://github.com/facebook/react/issues/28391

## Description

I have the following piece of code which should synchrounously render some react node inside dom NODE.

```
    const DOM = (
      <div
        {...attributesToProps(attrs)}
        className={cn(
          'p-[8px]',
          variant === 'theorem' ? 'border-blue-7 bg-blue-3' : '',
          variant === 'definition' ? 'border-violet-7 bg-violet-3' : '',
          variant === 'remark' ? 'border-red-7 bg-red-3' : '',
          variant === 'example' ? 'border-green-7 bg-green-3' : ''
        )}
      >
        <div
          className={cn(
            'absolute left-0 top-0 rounded-full bg-background p-[8px]',
            variant === 'theorem' ? 'text-blue-8' : '',
            variant === 'definition' ? 'text-violet-8' : '',
            variant === 'remark' ? 'text-red-8' : '',
            variant === 'example' ? 'text-green-8' : ''
          )}
          style={{
            transform: 'translate(calc(-50% - 1.5px), -50%)',
          }}
        >
          <MathPanelIcon variant={variant} />
        </div>
        <div className='flex flex-col gap-4'>
          <p className='!m-0 text-2xl font-semibold'>
            <TextGradient color={gradient as GradientColor}>
              {label}
            </TextGradient>
          </p>
          <div
            data-type='mathPanelContent'
            className='flex flex-col gap-4'
          ></div>
        </div>
      </div>
    );

    const container = document.createElement('div');
    const root = createRoot(container);
    flushSync(() => {
      root.render(DOM);
    });

    const dom = container.firstChild as HTMLElement;
    const contentDOM = dom.querySelector(
      '[data-type="mathPanelContent"]'
    ) as HTMLElement;
```


The problem is that it sometimes works and sometimes not. For example, here is works:
[![enter image description here][1]][1]


But here not:
[![enter image description here][2]][2]


  [1]: https://i.stack.imgur.com/qLb8v.png
  [2]: https://i.stack.imgur.com/YwKLR.png


Any ideas what differ these two cases?
