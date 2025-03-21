# Bug: React can leak the whole subtree when using contentEditable (reproduction sscce included)

> Issue #28370 - Created on 2/18/2024

> Original URL: https://github.com/facebook/react/issues/28370

## Description

There is a memory leak which seems to be a combination of `contenteditable` and CSS classes. I am not sure how CSS can affect React to produce leak, but I can't reproduce the same with plain JavaScript. Both code samples below.

Leads to massive memory leaks when content editable is a leaf of a deep subtree.

React version: 18.2.0

## Steps To Reproduce

1. Copy html to a file and open it with Chrome
2. Take a memory snapshot
3. Click on the "Toggle" button to mount subtree
4. Input `hello<Enter><Enter>world`
5. Click "Toggle" button to unmount subtree
6. Take a second memory snapshot
7. Compare 2 snapshots and filter by "detached"

Link to code example:

Here is the tiniest reproduction I can get. From the code it might seem that this is a browser issue, however (see second code snippet) I was not able to confirm it.
```html
<!DOCTYPE html>
<head>
  <script src="https://unpkg.com/react@18.2.0/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@18.2.0/umd/react-dom.production.min.js"></script>
  <style>
    .input {
      position: relative;
      width: 200px;
      border: 1px solid black;
    }

    /* Having this is important */
    .input:empty::before {
      position: absolute;
      content: attr(placeholder);
    }

    /*
    Having this selector regardless of class names will cause leaks.
    Comment out to observe leak gone.
    */
    .literally:empty+.anything {}
  </style>
</head>
<body>
  <div id="root"></div>
  <script>
    function Leak() {
      const [isVisible, setVisible] = React.useState(false);

      return React.createElement(
        'div',
        {
          className: 'leak'
        },
        [
          React.createElement(
            'button',
            {
              onClick: () => setVisible(!isVisible)
            },
            ['Toggle']
          ),
          isVisible && React.createElement(ContentEditable)
        ]
      );
    }

    function ContentEditable() {
      return React.createElement('div', {
        className: 'input',
        contentEditable: true,
        placeholder: "Placeholder"
      })
    }

    const root = ReactDOM.createRoot(document.querySelector('#root'));
    root.render(React.createElement(Leak));
  </script>
</body>
```

Here is how I tried to reproduce the same leak with plain JavaScript.
```html
<!DOCTYPE html>
<head>
  <style>
    .input {
      position: relative;
      width: 200px;
      border: 1px solid black;
    }

    /* Having this is important */
    .input:empty::before {
      position: absolute;
      content: attr(data-placeholder);
    }

    /*
    Having this selector regardless of class names will cause leaks.
    Comment out to observe leak gone.
    */
    .literally:empty+.anything {}
  </style>
</head>
<body>
  <button onclick="toggle()">Toggle</button>
  <div id="root"></div>
  <script>
    function toggle() {
      const div = document.querySelector("div.leak");

      if (div) {
        div.remove();
        return
      }

      const input = document.createElement('div');
      input.innerHTML = `
        <div class="leak">
          <div class="input" contenteditable="true" data-placeholder="Placeholder"></div>
        <div>
      `;

      document.querySelector("div#root").appendChild(input);
    }
  </script>
</body>
```

## The current behavior

The whole subtree staring from `div.leak` will leak as Detached HTMLDivElement. The actual node leaked is `div.input` however due to `.parentElement` references it leaks the whole subtrees. And the problem is that if subtree is deep enough it can cause massive memory leaks.

## The expected behavior

There are no Detached HTMLDivElements leaking.
