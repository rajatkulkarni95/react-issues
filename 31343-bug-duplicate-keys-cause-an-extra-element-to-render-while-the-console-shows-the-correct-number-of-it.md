# Bug: duplicate keys cause an extra element to render, while the console shows the correct number of items

> Issue #31343 - Created on 10/24/2024

> Original URL: https://github.com/facebook/react/issues/31343

## Description

When rendering a list with duplicate keys, React incorrectly renders an extra item, which is interactable, despite the console logging the correct number of items. This behavior occurs even though the data source has the correct number of items.

React version: ^18.0.0

## Steps To Reproduce

1. `$ npx create-react-app my-app`
2. `$ cd my-app`
3. Replace the contents of App.js with the code listed below
4. `$ npm run start`
5. Open the page in Google Chrome or Edge or any browser
6. Click one of the "Add record" button

```js
import { useState } from "react";

const initialRecords = [
  { id: 1, name: "John Wick", email: "john@wick" },
  { id: 2, name: "Hermione Granger", email: "hermione@granger" },
  { id: 3, name: "Harry Potter", email: "harry@potter" },
  { id: 3, name: "ID Dup", email: "id@duplicate" },
];

export default function App() {
  const [records, setRecords] = useState(initialRecords);

  const handleAddClick = () => {
    const newRecord = { id: 4, name: "New Record", email: "new@record" };
    setRecords((prev) => [newRecord, ...prev]);
  };

  return (
    <div>
      <button onClick={handleAddClick}>Add record</button>
      {records.map(({ id, name, email }) => (
        <div key={id}>
          <p>{id}</p>
          <p>{email}</p>
          <p>{name}</p>
        </div>
      ))}
    </div>
  );
}
```


Link to code example: https://codesandbox.io/p/sandbox/ylr42w

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
1. React renders an extra (phantom) item that duplicates an existing item (due to the duplicate key). And the count of extra item (id: 3) keeps increasing on every click.
2. This extra item is fully interactable (e.g., it responds to click events).
3. The console logs the correct number of items (5), but 6 items appear on the screen

## The expected behavior
1. The number of rendered items should match the actual number of items in the data array, regardless of key duplication.
2. If keys are not unique, React should throw a warning or handle it predictably (e.g., not render an extra item).
