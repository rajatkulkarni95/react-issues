# [React 19] useOptimistic is not updating its optimistic collection immediately

> Issue #31020 - Created on 9/22/2024

> Original URL: https://github.com/facebook/react/issues/31020

## Description

I have this component that I created where I'm testing useOptimistic and don't have a real backend to call to. So my data source is a variable in another module called messagesOnApi. I have a local state variable messagesRetrievedFromApi that I use to load the data from my fake api, messagesOnApi, and then when I call useOptimistic I pass the messagesRetrievedFromApi state variable as the first parameter.
When I make my update to the api data I add a delay but instead of my optimistic data updating immediately it only updates after the delay. Why? 
This is the github with entire source, https://github.com/PacktPublishing/Full-Stack-React-TypeScript-and-Node-2nd-Edition/blob/main/Chap5/components/src/OptimisticMessages.tsx. This is the main component.


```
import {
  useOptimistic,
  useState,
  MouseEvent,
  ChangeEvent,
  useTransition,
  useEffect,
} from "react";
import { Message, messagesOnApi } from "./MessagesData";

export function OptimisticMessages() {
  const [messagesRetrievedFromApi, setMessagesRetrievedFromApi] = useState<
    Message[]
  >([]);
  const [message, setMessage] = useState("");
  const [optimisticMessages, addOptimisticMessage] = useOptimistic<
    Message[],
    string
  >(messagesRetrievedFromApi, (currentMessages, message) => {
    const finalMessages = [
      ...currentMessages,
      { id: getNextId(currentMessages), message },
    ];
    return finalMessages;
  });
  const [_isPending, startTransition] = useTransition();

  useEffect(() => {
    const data = JSON.parse(JSON.stringify(messagesOnApi));
    setMessagesRetrievedFromApi(data);
  }, []);

  const addMessage = async (message: string) => {
    addOptimisticMessage(message);
    await new Promise((res) =>
      setTimeout(() => {
        messagesOnApi.push({
          id: getNextId(messagesOnApi),
          message,
        });
        res(null);
      }, 2000)
    );

    const data = JSON.parse(JSON.stringify(messagesOnApi));
    setMessagesRetrievedFromApi(data);
    setMessage("");
  };

  const onChange = (e: ChangeEvent<HTMLInputElement>) => {
    e.preventDefault();
    setMessage(e.target.value);
  };

  const onClick = async (e: MouseEvent<HTMLButtonElement>) => {
    e.preventDefault();

    startTransition(() => {
      addMessage(message);
    });
  };

  return (
    <div>
      <input value={message} onChange={onChange} />
      <button onClick={onClick}>add</button>
      <ul style={{ listStyleType: "none" }}>
        {optimisticMessages.map((m, i) => (
          <li key={i}>{m.message}</li>
        ))}
      </ul>
    </div>
  );
}

function getNextId(currentMessages: Message[]) {
  let id = 0;
  for (let i = 0; i < currentMessages.length; i++) {
    if (currentMessages[i].id > id) id = currentMessages[i].id;
  }
  id += 1;
  return id;
}
```
